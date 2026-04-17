**Tags:** #concept #nlp #ner #sequence-labelling
**Related:** [[Named Entity Recognition]], [[BIO Tagging Scheme]]

## Definition

BIOES (Begin-Inside-Outside-End-Single) extends BIO with explicit End and Single labels. **S**-TYPE marks a single-token entity; **E**-TYPE marks the final token of a multi-token entity.

> [!info] Key Intuition
> BIOES eliminates the ambiguity in BIO where a single-token entity looks like a two-token entity missing its I token. The explicit S and E labels give the model stronger supervision signals at entity boundaries.

## Core Mechanics

Label set for entity type X: `B-X`, `I-X`, `O`, `E-X`, `S-X`

With $k$ entity types → $4k + 1$ labels (vs $2k + 1$ for BIO).

**Valid transitions**:
- Single-token entity: `S-X`
- Multi-token entity: `B-X` → one or more `I-X` → `E-X`
- Non-entity: `O`

> [!example]- Worked Example
> Sentence: *"Apple CEO Tim Cook visited London."*
> BIO:   `B-ORG O B-PER I-PER O B-LOC O`
> BIOES: `S-ORG O B-PER E-PER O S-LOC O`
>
> "Apple" and "London" are now unambiguously single-token entities (S-), while "Tim Cook" clearly starts (B-) and ends (E-).

## Significance

BIOES typically yields modestly higher NER F1 than BIO because the richer label set provides more explicit boundary supervision, particularly benefiting CRF-based models.
