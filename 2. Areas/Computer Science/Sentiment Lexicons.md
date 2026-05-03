**Tags:** #concept #nlp #sentiment
**Related:** [[Sentiment Analysis]], [[VADER]], [[Opinion Mining]]

## Definition

A sentiment lexicon is a vocabulary of words annotated with their sentiment polarity (positive/negative) and often an intensity score. Lexicon-based sentiment analysis aggregates these word scores to infer document or sentence polarity without any training data.

> [!info] Key Intuition
> Lexicon-based SA trades recall for transparency: it can explain exactly which words drove its score, but fails whenever a word's sentiment depends entirely on context.

## Core Mechanics

Common lexicons:
| Lexicon | Coverage / domain | Scores |
|---|---|---|
| **Bing Liu's Opinion Lexicon** | ~6,800 words, general | binary pos/neg |
| **AFINN** | ~3,300 words, general | –5 to +5 integer (graded intensity) |
| **NRC Emotion Lexicon** | general | multi-label: anger, anticipation, disgust, fear, joy, sadness, surprise, trust + pos/neg |
| **Loughran–McDonald** | financial reporting | binary, domain-tuned ("liability", "capital" treated as neutral) |
| **SentiWordNet** | WordNet senses | pos/neg/obj per sense |
| **VADER** | social media tuned | compound score with negation/intensifier handling |

The choice of lexicon should align with **domain** and **interpretive goal**. A general lexicon misclassifies financial text systematically; an emotion lexicon enables emotion classification rather than mere polarity.

**Scoring pipeline**:
1. Tokenise and normalise the text
2. Look up each token in the lexicon
3. Handle negation windows (*"not good"* flips polarity)
4. Handle intensifiers (*"very good"* amplifies score)
5. Aggregate (sum or mean) to produce a document score

> [!example]- Worked Example
> Sentence: *"This film is not particularly bad."*
> - "bad" → AFINN –3
> - "not" → flip sign → +3
> - "particularly" → intensifier → no change (already flipped)
> - Final: weakly positive (+3 out of max ≈ +5 per token)

> [!warning] Common Misconception
> Domain mismatch is the biggest failure mode. *"This bond is sick"* (finance: risky) vs *"This track is sick"* (music: excellent) have opposite polarities — a general lexicon will score both identically.
