# NER Feature Extraction — Presentation Script & Technical Reference

---

## Script

Raw news articles are unstructured text — noisy, inconsistent, and full of words that carry no real signal for downstream tasks like topic modelling or document similarity.

The feature extraction step addresses this by running Named Entity Recognition over every clean article. We use **dslim/bert-base-NER**, a BERT model fine-tuned on the CoNLL-2003 benchmark, to detect four entity types: persons, organisations, locations, and miscellaneous.

The input is a single field — the article **body string**. Because BERT has a hard 512-subtoken limit, we split long articles into overlapping 400-word chunks, run inference on each, and stitch the results back together. Entity boundaries are then snapped to whole words to prevent mid-word cuts from BERT's subword tokeniser.

The output is a **list of dicts** — one per entity — each containing the surface text, its label, and its character offsets in the original body. That list is stored alongside the article and passed to the preprocessing step for downstream modelling.

---

## Full Technical Reference


### 1. Where Feature Extraction Sits in the Pipeline

The system has four sequential stages. Each stage reads from one MongoDB collection and writes to another:

```
nlp_raw.articles          ← scraped from 40+ RSS feeds
        ↓  clean_job
nlp_clean.articles        ← quality-ranked, normalised articles
        ↓  classify_job   ← THIS IS WHERE FEATURE EXTRACTION HAPPENS
nlp_ner.ner_articles      ← clean articles + extracted entities
        ↓  evaluate_job
nlp_models.model_runs     ← evaluation metrics
```

Feature extraction lives entirely inside the **classify job**.

---

### 2. Inputs and Outputs

#### Input

One field from a `nlp_clean.articles` document:

```python
body: str
# "Barack Obama visited New York yesterday to meet UN officials."
```

Everything else in the article document (url, title, feed, pub date, etc.) is carried through unchanged.

#### Output — Feature Extraction (`ner_extractor.py`)

```python
entities: list[dict]

[
    {"text": "Barack Obama", "label": "PER",  "start": 0,  "end": 12},
    {"text": "New York",     "label": "LOC",  "start": 21, "end": 29},
    {"text": "UN",           "label": "ORG",  "start": 42, "end": 44},
]
```

Each dict has exactly four keys:

| Key | Type | Description |
|-----|------|-------------|
| `text` | `str` | Surface form of the entity as it appears in the body |
| `label` | `str` | Entity type: `PER`, `ORG`, `LOC`, or `MISC` |
| `start` | `int` | Character offset (start) in the normalised body string |
| `end` | `int` | Character offset (end) in the normalised body string |

`body[start:end]` always equals `text` — this is guaranteed by word-boundary snapping (see §4).

#### Output — Preprocessing (`ner_text_builder.py`)

Built from `body` + `entities`, stored as a second new field:

```python
ner_preprocessed_text: str
# "PER_Barack_Obama visit LOC_New_York ORG_UN official"
```

This is the input to TF-IDF and downstream modelling — not the raw entities list.

#### What gets written to `nlp_ner.ner_articles`

The original clean article document, plus two new fields:

```python
{
    # ...all original fields: url, title, feed, body, clean_text, ...
    "entities":              list[dict],   # ← from ner_extractor
    "ner_preprocessed_text": str,          # ← from ner_text_builder
}
```

---

### 3. Step-by-Step Execution Flow

Orchestrated by `src/jobs/classify_job.py`:

```
1. Fetch unprocessed clean articles (not yet in nlp_ner)
   └─ batch size: 64 articles

2. For each article body:

   ner_extractor.py
   ├─ normalize whitespace:  " ".join(body.split())
   ├─ if len(words) > 400:
   │    split into overlapping 400-word chunks (40-word overlap)
   │    run BERT inference per chunk
   │    shift offsets back to absolute positions in the full body
   │    deduplicate entities seen in overlap windows
   │  else:
   │    run BERT inference directly on the full text
   └─ snap every entity boundary to whole words (_snap_to_word)

   ner_text_builder.py
   ├─ sort entities by start offset (descending, to avoid index shifting)
   ├─ replace each span: body[start:end] → LABEL_surface_text
   ├─ stash NER tokens (regex: PER_|ORG_|LOC_|MISC_ prefixed tokens)
   ├─ run standard preprocessing (lemmatize, remove stopwords)
   └─ restore NER tokens — they are never touched by the lemmatizer

3. Accumulate results; flush to nlp_ner.ner_articles every 256 articles
```

Key source files:

| File | Role |
|------|------|
| `src/jobs/classify_job.py` | Batch orchestration, DB reads/writes |
| `src/features/ner_extractor.py` | BERT inference, chunking, alignment |
| `src/preprocessing/ner_text_builder.py` | Entity token substitution + preprocessing |
| `src/db/repositories.py` | `get_unprocessed_clean_articles`, `insert_ner_articles` |

---

### 4. The Chunking and Alignment Problem

**Why chunking is necessary:**
BERT's WordPiece tokeniser converts words into subtokens. A single word like "cryptocurrency" may become 4 subtokens. A 400-word article can easily exceed BERT's hard limit of 512 subtokens, causing silent truncation — the model would simply never see the end of the article.

**The solution (400-word chunks, 40-word overlap):**

```
Article words: [w0 w1 w2 ... w399 | w360 w361 ... w759 | w720 ...]
                └── chunk 1 ──────┘  └── chunk 2 ────────┘
                              └─ 40-word overlap ─┘
```

- Each chunk is at most 400 words — safe under the 512-subtoken limit
- The 40-word overlap ensures entities that fall exactly on a chunk boundary are not missed
- Offsets from each chunk are shifted by the chunk's start position in the full body
- A `seen: set[tuple[start, end, label]]` deduplicates entities found twice in the overlap

**Why word-boundary snapping (`_snap_to_word`) is necessary:**
WordPiece splits words into subtokens (`Barack → [Ba, ##rack]`). When HuggingFace reassembles spans from subtoken offsets, the start or end may land inside a word. `_snap_to_word` walks the start backward and the end forward until it hits whitespace, guaranteeing `body[start:end] == entity.text`.

---

### 5. BERT — The Base Model

**What it is:**
BERT (Bidirectional Encoder Representations from Transformers, Google 2018) is a Transformer encoder pre-trained on Wikipedia and BooksCorpus.

**Architecture (bert-base):**

| Parameter | Value |
|-----------|-------|
| Layers | 12 |
| Attention heads | 12 |
| Hidden size | 768 |
| Parameters | ~110M |
| Tokeniser | WordPiece (30,522 vocab) |
| Max input | 512 subtokens |

**Pre-training tasks:**
- **MLM (Masked Language Modelling):** 15% of tokens are masked at random; the model learns to predict them using both left and right context
- **NSP (Next Sentence Prediction):** the model learns whether two sentences are consecutive

**Key property — bidirectionality:**
Unlike GPT (left-to-right only), BERT reads the entire sentence simultaneously. The representation of a word is informed by all words around it. This means "bank" in "river bank" gets a different embedding than "bank" in "bank loan" — critical for disambiguation.

**Tokeniser:**
WordPiece breaks unknown or rare words into subword pieces:
```
"New York"  → [New] [York]
"Barack"    → [Ba] [##rack]
"unrelated" → [un] [##related]
```
`##` marks continuation pieces. This is why a 400-word article can exceed 512 subtokens.

---

### 6. BERT-NER — The Fine-Tuned Model

**Model:** `dslim/bert-base-NER` (HuggingFace)
**Base:** `bert-base-cased` — cased because capitalisation matters for NER ("apple" ≠ "Apple")
**Fine-tuned on:** CoNLL-2003 (~14,000 training sentences of Reuters newswire, manually labelled)

**What fine-tuning adds:**
A single linear classification head on top of BERT's final hidden layer:
```
hidden state (768-dim) → linear layer → 9 classes
```

The 9 classes are BIO tags:

| Tag    | Meaning                      |
| ------ | ---------------------------- |
| O      | Not an entity                |
| B-PER  | Beginning of a person name   |
| I-PER  | Inside a person name         |
| B-ORG  | Beginning of an organisation |
| I-ORG  | Inside an organisation       |
| B-LOC  | Beginning of a location      |
| I-LOC  | Inside a location            |
| B-MISC | Beginning of a misc entity   |
| I-MISC | Inside a misc entity         |

**BIO tagging example:**
```
Barack  Obama   visited  New    York
B-PER   I-PER   O        B-LOC  I-LOC
```

**`aggregation_strategy="simple"`:**
HuggingFace's pipeline merges consecutive B-/I- tags into a single span automatically, returning `{entity_group, score, word, start, end}` instead of per-token tags. "Simple" takes the score of the first token (B-) rather than averaging — this is a minor implementation detail, not a quality concern.

**Entity types:**

| Label | Examples |
|-------|---------|
| PER | Barack Obama, Elon Musk, Dr. Dre |
| ORG | Apple Inc., United Nations, Tesla |
| LOC | New York, California, France |
| MISC | FIFA World Cup, English, iPhone |

---

### 7. Before / After: Feature Extraction

| Raw `body`                                   | `entities` output                                                             |
| -------------------------------------------- | ----------------------------------------------------------------------------- |
| `"Barack Obama visited New York."`           | `[{PER, "Barack Obama", 0, 12}, {LOC, "New York", 21, 29}]`                   |
| `"Apple acquired Beats in California."`      | `[{ORG, "Apple", 0, 5}, {ORG, "Beats", 15, 20}, {LOC, "California", 24, 34}]` |
| `"The FIFA World Cup was held in Qatar."`    | `[{MISC, "FIFA World Cup", 4, 18}, {LOC, "Qatar", 31, 36}]`                   |
| `"Elon Musk announced a factory in Berlin."` | `[{PER, "Elon Musk", 0, 9}, {LOC, "Berlin", 32, 38}]`                         |

---

### 8. Evaluation

Two evaluations run after NER processing (`src/jobs/evaluate_job.py`):

**Separability (primary — research metric):**
- Takes 200 articles, computes pairwise TF-IDF cosine similarity for `clean_text` vs `ner_preprocessed_text`
- Lower mean similarity = documents are more discriminable from each other
- Returns: `clean_avg_similarity`, `ner_avg_similarity`, `improvement_pct`, `verdict`

**CoNLL-2003 benchmark (model validation):**
- Runs the NER model on 500 held-out CoNLL-2003 sentences
- Computes strict entity-level Precision / Recall / F1 per entity type via `seqeval`
- Detects model regressions before they reach production

Results are stored in `nlp_models.model_runs`.

---

### 9. Likely Q&A

**Q: Why BERT and not a simpler model like spaCy's rule-based NER?**
BERT produces context-aware token representations — the same word gets a different embedding depending on its surroundings. This is critical for ambiguous entities ("Apple" the company vs "apple" the fruit, "Washington" the person vs the city). spaCy's `en_core_web` models use simpler token-level features and are faster but less accurate on news text.

**Q: Why bert-base and not bert-large?**
bert-large has 24 layers and 340M parameters — roughly 3× the compute cost. For a token-classification task like NER on newswire text, bert-base fine-tuned on CoNLL-2003 already achieves F1 ~91% on the benchmark. The marginal gain from bert-large does not justify the inference cost in a batch pipeline.

**Q: Why 400-word chunks specifically?**
English words average ~1.3 subtokens each. 400 words × 1.3 = ~520 subtokens. Subtracting the 2 special tokens (`[CLS]`, `[SEP]`), this gives ~518 — just under the 512 limit with a small safety margin. Tested empirically: no truncation observed at 400 words.

**Q: What is the 40-word overlap for?**
Entities can span a chunk boundary. Without overlap, "New York Times" split across chunks would be detected as "York Times" (partial) or missed entirely. 40 words is wide enough to catch any realistic multi-word entity.

**Q: Does `aggregation_strategy="simple"` affect accuracy?**
Minimally. The alternative is `"average"` (averages subtoken scores) or `"max"`. For CoNLL-2003 style entities, `"simple"` and `"average"` produce nearly identical span boundaries. We use `"simple"` because it is the HuggingFace default for this model.

**Q: Why store character offsets instead of token indices?**
Character offsets are stable regardless of tokeniser version or configuration. They work directly with the raw `body` string — `body[start:end]` gives the entity text without any tokeniser dependency. Token indices would be fragile to tokeniser changes.

**Q: What happens to non-English articles?**
The pipeline has an `ENGLISH_ONLY=true` flag. Non-English articles are filtered out during the clean job and never reach the classify job. `dslim/bert-base-NER` was trained on English CoNLL-2003 only — applying it to other languages would degrade accuracy significantly.

**Q: How do we know it actually improves downstream performance?**
The separability evaluation (`separability_eval.py`) quantifies this: it measures whether NER-preprocessed documents are more distinguishable from each other than plain clean text, using TF-IDF cosine similarity as a proxy. A lower mean pairwise similarity after NER preprocessing indicates better signal for downstream tasks like clustering or classification.
