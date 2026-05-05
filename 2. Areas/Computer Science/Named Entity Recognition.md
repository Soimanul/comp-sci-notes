**Tags:** #hub #nlp #ner #sequence-labelling
**Related:** [[Natural Language Processing]], [[POS Tagging]], [[BIO Tagging Scheme]]

## Overview

Named Entity Recognition (NER) identifies **spans** of text that refer to real-world entities and assigns each span a semantic type (person, organisation, location, date, …). Unlike POS tagging, the unit of prediction is a multi-token span, and the label space is **referential**, not grammatical. Mathematically the model looks identical to POS tagging — same HMM, same Viterbi — but the semantics, evaluation, and error sources differ.

> [!abstract]- TL;DR
> NER is span-based structured prediction. The IOB/BIO scheme reduces span detection to per-token labelling so that the same probabilistic machinery used for POS can be reused. Classical solutions are HMMs decoded with Viterbi; modern systems use CRFs and BERT-based token classifiers. Evaluation is **strict span precision/recall** — partial matches do not count.

## Knowledge Map

### 1. The Task
- [[Opinion Mining]]  
*(reference for "structured semantic extraction")*
- [[POS vs NER Comparison]]

### 2. Span-as-Sequence Encoding
- [[BIO Tagging Scheme]]
- [[BIOES Tagging Scheme]]

### 3. Classical Probabilistic Approach
- [[HMM-Based NER]]
- [[Viterbi Algorithm]]

### 4. Discriminative and Neural Approaches
- [[CRF for Sequence Labelling]]
- [[BERT for NER]]

### 5. Evaluation
- [[Span-Based Evaluation]]

> [!question]- Common Exam Questions
> - Why can NER not be reduced to independent token classification?
> - How does the IOB/BIO scheme convert span detection into a sequence-labelling problem?
> - State the HMM joint model used for NER and explain the role of transition vs emission probabilities.
> - Why is partial-match credit excluded from standard NER evaluation?
> - What changes between POS tagging and NER if the model architecture is the same?
> - How do CRFs improve over HMMs for this task?

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** NER differs from POS tagging in that:
- A. NER predicts *referential* labels over *spans*; POS predicts grammatical categories per token
- B. NER cannot use HMMs
- C. NER uses no embeddings
- D. NER does not need labels

> [!success]- Answer
> **A.** Same machinery, different semantics — and crucially span-based evaluation.

**2.** The BIO scheme encodes spans by:
- A. Marking the first token of an entity *B-X*, internal tokens *I-X*, and non-entity tokens *O*
- B. Marking only the first token
- C. Using only one tag per sentence
- D. Marking entities with regex

> [!success]- Answer
> **A.** This converts the span-detection problem into a per-token labelling problem solvable by sequence models.

**3.** BIOES extends BIO by adding which tags?
- A. *E-X* (end of multi-token entity) and *S-X* (single-token entity)
- B. *F-X* (first) and *L-X* (last)
- C. *D-X* (date)
- D. *N-X* (none)

> [!success]- Answer
> **A.** BIOES gives the tagger more granular signal at span boundaries.

**4.** Why is *partial* span credit excluded from standard NER evaluation?
- A. Partial matches reward systems that hallucinate boundaries; downstream consumers need exact spans for linking and aggregation
- B. Partial matches are computationally hard
- C. Partial matches are never useful
- D. Tradition only

> [!success]- Answer
> **A.** Strict span match is the operational standard (CoNLL-2003 style).

**5.** A common BIO error is *I-PER* appearing at the start of an entity. The cleanest fix is:
- A. Constrain decoding to disallow *I-X* unless preceded by *B-X* or *I-X* of the same type
- B. Use a bigger model
- C. Drop BIO and use IO
- D. Train longer

> [!success]- Answer
> **A.** Decoder-side constraints (legal transitions) are an easy structural fix; CRFs encode them as transition costs.

**6.** A CRF over BIO labels improves on an HMM mainly because it:
- A. Conditions on the entire input (rich features) and is trained discriminatively without independence assumptions
- B. Is faster
- C. Uses softmax
- D. Removes Viterbi

> [!success]- Answer
> **A.** Discriminative + global feature access = better tagging when features matter (capitalization, gazetteers, surrounding tokens).

**7.** BERT for NER works by:
- A. Encoding the sentence with a pretrained Transformer and applying a per-token classification head; sometimes followed by a CRF for transition consistency
- B. Computing TF–IDF
- C. Using regex
- D. Using HMM emissions

> [!success]- Answer
> **A.** Standard recipe: BERT (or RoBERTa) + linear layer + optional CRF on top of the logits.

**8.** Why are gazetteers (entity dictionaries) still useful in modern NER?
- A. They inject high-precision priors for known names and rare classes (e.g., new diseases) that the model has seen rarely
- B. They replace the model
- C. They eliminate spans
- D. They define BIO

> [!success]- Answer
> **A.** Gazetteers + neural models is a strong hybrid for industry NER.

**9.** A model tags *"Apple announced…"* as *B-PER* instead of *B-ORG*. The structural reason is most likely:
- A. The model has not seen sufficient evidence of *Apple* as ORG in this sentential context
- B. BIO is broken
- C. ORG is not a class
- D. *Apple* is OOV

> [!success]- Answer
> **A.** Disambiguating *Apple* (PER vs ORG vs FRUIT) requires contextual signals; BERT-class models do this well, simpler models often miss.

**10.** A nested entity like *"University of California, Berkeley"* (ORG with location inside) is tricky because:
- A. Vanilla BIO assigns one tag per token and cannot represent overlapping/nested spans natively
- B. BIO is too long
- C. Nested entities are illegal
- D. CRFs cannot tag them

> [!success]- Answer
> **A.** Nested NER requires special schemes (stacked BIO, span-classification models, or graph-based decoders).

**11.** Span precision is computed as:
- A. # exact-match predicted spans / # predicted spans
- B. Tokens correctly tagged / total tokens
- C. # entities / # documents
- D. Boundary tokens correct / total

> [!success]- Answer
> **A.** Strict at the *span* level — wrong type or wrong boundaries both count as errors.

**12.** Why does token-level accuracy *overstate* NER performance?
- A. The dominant *O* class inflates accuracy regardless of span quality; only span-level metrics expose true performance
- B. Tokens are small
- C. Accuracy excludes *O*
- D. BIO removes accuracy

> [!success]- Answer
> **A.** Most tokens are O; trivial baselines look great on accuracy. Use precision/recall/F1 on spans instead.

**13.** An HMM-based NER tagger struggles with rare entity types because:
- A. Emission and transition counts for rare types are tiny, leading to noisy probability estimates
- B. HMMs cannot tag rare entities
- C. BIO breaks
- D. Viterbi diverges

> [!success]- Answer
> **A.** Standard data-sparsity issue; smoothing helps marginally.

**14.** Which feature is *most* characteristic of well-engineered classical NER systems?
- A. Capitalization, prefix/suffix shape, gazetteer membership, and POS context
- B. Document length
- C. Cosine similarity
- D. TF–IDF

> [!success]- Answer
> **A.** These are the canonical NER features (Ratinov & Roth) — orthography is a strong signal for English NER.

**15.** A pipeline applying NER followed by entity linking depends on NER's:
- A. Span boundaries — wrong boundaries propagate as wrong KB lookups
- B. Tokenization speed
- C. Model size
- D. Training corpus

> [!success]- Answer
> **A.** Linking is span-level; partial spans silently corrupt downstream KB matches.

**16.** Why is BERT more robust than CRF on cross-domain NER?
- A. Pretraining on massive corpora gives BERT lexical and contextual generalization that hand-crafted CRF features lack
- B. CRF cannot generalize
- C. BERT removes BIO
- D. BERT uses softmax

> [!success]- Answer
> **A.** Pretraining is the durable advantage; for a fresh domain you fine-tune BERT rather than re-engineer features.

**17.** Active learning helps NER specifically when:
- A. Labels are expensive and entity classes are rare; selecting uncertain examples maximizes label efficiency
- B. The corpus is small
- C. The model is fast
- D. Spans are short

> [!success]- Answer
> **A.** Targeted annotation pays off; random sampling wastes label budget on easy cases.

**18.** A practitioner reports F1=0.9 token accuracy but F1=0.6 on spans. Diagnose:
- A. The model labels most O tokens correctly but misses or mis-bounds many entities — focus on span-level errors
- B. The model is broken
- C. Token-level metrics are wrong
- D. BIO is unsupported

> [!success]- Answer
> **A.** A common pattern; the metric mismatch is the diagnostic clue.

**19.** Multi-task learning of NER + POS often helps because:
- A. POS provides syntactic context useful for entity boundary detection; shared representations improve generalization
- B. POS is supervision for NER
- C. POS replaces NER
- D. POS uses BIO

> [!success]- Answer
> **A.** Joint training is a low-cost way to inject inductive bias.

**20.** *"Steve Jobs founded Apple in California."* A perfect tagger should output (in BIO):
- A. B-PER I-PER O B-ORG O B-LOC
- B. B-PER B-PER O B-ORG O B-LOC
- C. B-LOC I-LOC O B-PER O B-ORG
- D. O O O B-ORG O O

> [!success]- Answer
> **A.** *Steve* begins a multi-token PER (so I-PER on *Jobs*); *Apple* and *California* are single-token entities, hence B-ORG and B-LOC.

**21.** A failure mode of BERT-NER on legal documents is:
- A. Domain-specific entity types and conventions absent from pretraining (citations, statutes) require domain pretraining or careful fine-tuning
- B. BERT cannot read legal text
- C. BIO is illegal in law
- D. BERT outputs probabilities

> [!success]- Answer
> **A.** Pretraining bias is real; LEGAL-BERT, BioBERT, etc. exist for exactly this reason.

**22.** The deepest similarity between POS tagging and NER is:
- A. Both are sequence-labelling problems amenable to HMM/CRF/BERT pipelines; the *labels and evaluation* differ but the *machinery* is shared
- B. They have identical labels
- C. NER replaces POS
- D. POS does spans

> [!success]- Answer
> **A.** Same algorithms, different label spaces and metrics.
