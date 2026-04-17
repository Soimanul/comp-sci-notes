**Tags:** #concept #nlp #sentiment
**Related:** [[Sentiment Analysis]], [[Opinion Mining]]

## Definition

Subjectivity refers to text expressing personal opinions, beliefs, or emotions; objectivity refers to factual, verifiable statements. Subjectivity detection is a prerequisite step in sentiment analysis pipelines — only subjective text carries sentiment worth classifying.

> [!info] Key Intuition
> "The laptop weighs 1.4 kg" is objective; "The laptop feels heavy" is subjective. Sentiment classifiers trained on objective text produce meaningless results.

## Core Mechanics

Subjectivity can be detected via:
- **Lexical clues** — presence of opinion words (*amazing*, *terrible*, *unfortunately*)
- **Syntactic patterns** — first-person expressions, modal verbs (*should*, *might*)
- **Classifier models** — trained binary classifier on labelled subjective/objective sentences

Subjectivity operates at multiple granularities:
- **Document level** — is this an editorial or a news article?
- **Sentence level** — is this sentence opinionated?
- **Phrase level** — which span carries the subjective load?

> [!example]- Worked Example
> Objective: *"The iPhone 15 ships with a 48MP main sensor."*
> Subjective: *"The iPhone 15 takes breathtakingly good photos."*
> A sentiment pipeline would skip the first sentence and classify the second as positive.

> [!warning] Common Misconception
> Negative sentiment ≠ subjectivity. "The company lost €3M last quarter" is objective and negative. Subjectivity is about whether the text encodes a personal stance, not whether it contains bad news.
