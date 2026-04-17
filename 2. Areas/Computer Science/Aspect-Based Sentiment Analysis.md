**Tags:** #concept #nlp #sentiment
**Related:** [[Sentiment Analysis]], [[Opinion Mining]]

## Definition

Aspect-Based Sentiment Analysis (ABSA) extracts the specific features (aspects) of an entity that are being evaluated, and determines the sentiment expressed toward each aspect independently. It goes beyond document-level polarity to produce per-attribute opinion summaries.

> [!info] Key Intuition
> Document-level SA answers "is this review positive?" — ABSA answers "what does the reviewer think about the battery, the screen, and the price, separately?"

## Core Mechanics

ABSA pipeline stages:
1. **Aspect term extraction** — identify opinion targets (*"battery life"*, *"delivery speed"*)
2. **Aspect category detection** — map terms to abstract categories (*battery life → BATTERY*)
3. **Aspect sentiment classification** — assign polarity to each extracted aspect

**Approaches**:
- **Rule/dictionary-based** — dependency parse + opinion lexicon lookup
- **ML-based** — sequence tagger (CRF, BiLSTM) for aspect extraction; classifier for sentiment
- **End-to-end neural** — joint models (e.g., BERT fine-tuned on SemEval ABSA data) that extract aspects and classify their sentiment in one pass

> [!example]- Worked Example
> Review: *"Great camera but the battery drains in 3 hours."*
> | Aspect | Sentiment |
> |---|---|
> | camera | positive |
> | battery | negative |
> A document classifier would output "mixed" and lose both actionable signals.

> [!warning] Common Misconception
> Aspect terms are not always noun phrases. Implicit aspects occur frequently: *"It broke after a week"* implies a negative aspect on *durability* without ever stating the word.
