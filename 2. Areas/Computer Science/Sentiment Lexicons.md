**Tags:** #concept #nlp #sentiment
**Related:** [[Sentiment Analysis]], [[VADER]], [[Opinion Mining]]

## Definition

A sentiment lexicon is a vocabulary of words annotated with their sentiment polarity (positive/negative) and often an intensity score. Lexicon-based sentiment analysis aggregates these word scores to infer document or sentence polarity without any training data.

> [!info] Key Intuition
> Lexicon-based SA trades recall for transparency: it can explain exactly which words drove its score, but fails whenever a word's sentiment depends entirely on context.

## Core Mechanics

Common lexicons:
| Lexicon | Coverage | Scores |
|---|---|---|
| **SentiWordNet** | WordNet senses | pos/neg/obj per sense |
| **BING Liu's Opinion Lexicon** | ~6,800 words | binary pos/neg |
| **AFINN** | ~3,300 words | –5 to +5 integer |
| **VADER** | social media tuned | compound score |

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
