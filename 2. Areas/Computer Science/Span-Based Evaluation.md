**Tags:** #concept #nlp #ner #evaluation
**Related:** [[Named Entity Recognition]], [[Evaluation Metrics for Classifiers]]

## Definition

NER evaluation is **span-based and strict**. A predicted entity counts as correct only if **both the boundaries and the entity type** match the gold annotation exactly. Partial overlaps receive **zero credit**.

> [!info] Key Intuition
> NER is not multi-class classification of tokens — it is structured extraction of typed spans. Token-level accuracy hides boundary mistakes that ruin downstream extraction; span-level metrics expose them.

## Metrics

Given gold spans $G$ and predicted spans $P$:

- **Precision** = $\dfrac{|G \cap P|}{|P|}$ — fraction of predicted spans that are correct.
- **Recall** = $\dfrac{|G \cap P|}{|G|}$ — fraction of true spans that are recovered.
- **F1** = harmonic mean of precision and recall (the headline NER number).

A "match" requires (start, end, type) to all coincide.

> [!example]- Worked Example
> Gold: *"New York City"* → B-LOC I-LOC I-LOC.
> Prediction A: *"New York"* → B-LOC I-LOC. **Wrong** — boundary mismatch, no credit.
> Prediction B: *"New York City"* labelled ORG. **Wrong** — type mismatch, no credit.
> Prediction C: *"New York City"* labelled LOC. **Correct**.

## Why Strict Evaluation

Downstream uses (entity linking, relation extraction, knowledge-graph population) need anchors that are exactly right. A nearly-correct boundary often points to the wrong real-world referent — *"Bank of America"* is one organisation; *"Bank"* and *"of America Tower"* are not.

## Sources of Error

| Error | Description |
|---|---|
| **Boundary error** | Span starts or ends at the wrong token. |
| **Type confusion** | Span boundaries correct, label wrong (PER vs ORG). |
| **Data sparsity** | Rare names never seen in training. |
| **Contextual ambiguity** | Same surface form, different referent in different sentences. |
| **Nested entities** | *"Bank of America Tower"* — ORG inside LOC. Single-label IOB cannot represent both. |

Each error type maps back to an independence assumption in the model: boundary errors come from weak transition modelling, type confusion from emission ambiguity, nested-entity failures from the single-label-per-token encoding.

> [!warning] Common Misconception
> Token-level F1 (treating the IOB labels as multi-class targets) often looks much higher than entity-level F1. They measure different things; only entity-level numbers should be reported as NER performance.

## Significance

The strict evaluation rule is what enforces **structural** modelling. Any NER pipeline that optimises token accuracy without checking entity-level F1 will overfit to the dominant **O** label and look much better than it is in deployment.
