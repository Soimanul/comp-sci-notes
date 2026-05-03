**Tags:** #concept #nlp #ner #pos
**Related:** [[Named Entity Recognition]], [[POS Tagging]], [[HMM-Based NER]], [[HMM-Based POS Tagger]]

## Definition

POS tagging and NER use the **same probabilistic machinery** — HMM, CRF, BiLSTM-CRF, transformer-CRF — but differ in three dimensions: **label space**, **error type**, and **evaluation**. Knowing where they overlap and where they diverge clarifies what the model is actually learning.

> [!info] Key Intuition
> Architecturally identical, semantically different. The model says "given a sentence, output a tag sequence" in both cases — but the meaning of the tags and the cost of getting them wrong are not the same.

## Side-by-Side

| Dimension | POS Tagging | NER |
|---|---|---|
| **Label space** | Grammatical categories (NOUN, VERB, …) | Referential / semantic types (PER, ORG, LOC, …) |
| **Unit of prediction** | Single token | Multi-token **span** (encoded via IOB/BIO at token level) |
| **Information needed** | Local syntactic context | Local context + world knowledge / gazetteers |
| **Tagset size** | Closed, ~17 (Universal) to ~45 (PTB) | Open in principle; small in BIO with $2K+1$ labels for $K$ types |
| **Error type** | Tag misclassification | Boundary mismatch **+** type confusion |
| **Evaluation** | Token accuracy | Strict span precision / recall / F1 |
| **Out-of-vocabulary handling** | Suffix / morphology heuristics | Capitalisation, gazetteers, character features critical |

## Why the Same Model Reaches Different Performance

- POS tagging benefits from **closed grammatical regularities** — verbs follow subjects, determiners precede nouns. Bigram transitions carry a lot of signal.
- NER tagging needs **referential evidence** — *"Washington"* is grammatically a proper noun, but whether it is PER, LOC, or ORG depends on context the HMM can barely see.

Result: HMM-based POS taggers reach competitive accuracy with simple features; HMM-based NER lags neural systems by a much larger margin because the task needs richer features.

## What Carries Over

- Structured prediction framing.
- HMM joint model with transition / emission factorisation.
- Viterbi decoding.
- Smoothing / unknown-word handling at the emission level.
- The conceptual leap from independent classification to sequence labelling.

## What Does Not Carry Over

- Evaluation choice (strict span F1 vs token accuracy).
- Feature engineering priorities (NER lives or dies on capitalisation, gazetteers, word shape).
- Tolerance for boundary errors (catastrophic in NER, irrelevant in POS).

## Significance

This comparison is a clean example of how **the same architecture changes meaning when the label space changes**. Recognising it explains why later NER work invested heavily in CRFs (richer features) and transformers (deeper context) while POS tagging was considered "essentially solved" by HMMs much earlier.
