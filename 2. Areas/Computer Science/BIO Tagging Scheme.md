**Tags:** #concept #nlp #ner #sequence-labelling
**Related:** [[Named Entity Recognition]], [[BIOES Tagging Scheme]], [[CRF for Sequence Labelling]]

## Definition

The BIO tagging scheme (Begin-Inside-Outside) encodes named entity spans as token-level labels: **B**-TYPE marks the first token of an entity of TYPE, **I**-TYPE marks continuation tokens, and **O** marks non-entity tokens.

> [!info] Key Intuition
> BIO converts a span-detection problem into a sequence classification problem — every token gets exactly one label, making the output compatible with standard sequence models.

## Core Mechanics

Label set for entities PERSON, ORG, LOC:
`B-PER`, `I-PER`, `B-ORG`, `I-ORG`, `B-LOC`, `I-LOC`, `O`

With $k$ entity types, BIO generates $2k + 1$ labels.

**Transition constraints** (enforced by CRF or model):
- `I-X` must follow `B-X` or `I-X` (same type) — never `O` or a different type
- `B-X` can follow anything

> [!example]- Worked Example
> Sentence: *"Apple CEO Tim Cook visited London."*
> Labels: `B-ORG O B-PER I-PER O B-LOC O`
>
> "Tim Cook" spans two tokens: B-PER for "Tim", I-PER for "Cook".

> [!warning] Common Misconception
> `I-X` after `O` is an illegal transition in BIO — it implies a continuation without a beginning. Models without explicit transition constraints (e.g., vanilla softmax) can produce this, corrupting entity span extraction. A CRF layer prevents it.
