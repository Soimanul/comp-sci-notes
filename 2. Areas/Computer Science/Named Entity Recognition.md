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
