**Tags:** #concept #nlp #sentiment
**Related:** [[Lexicon Scoring]], [[Sentiment Lexicons]], [[VADER]]

## Definition

Lexicon-based sentiment scoring sums per-word polarity values, ignoring the structural way words combine. The aggregation breaks whenever sentiment depends on **composition** rather than additive lexical evidence.

> [!info] Key Intuition
> Counts are additive; meaning is not. *"good"* and *"not good"* contain the same positive token, but only the first carries positive sentiment.

## The Negation Patch

A common correction introduces a negation operator that reverses polarity within a window:

$$\text{score}(\text{not } w) = -\text{score}(w)$$

[[VADER]] and similar systems extend this with intensifier and diminisher modifiers (*"very bad"*, *"slightly good"*). These patches improve accuracy but do not change the underlying assumption that sentiment is lexical.

## Other Compositional Failures

| Failure mode | Example | What lexicon scoring misses |
|---|---|---|
| Negation scope | *"I do not think this is good"* | Negation crosses several tokens |
| Sarcasm | *"Oh great, another bug"* | Surface words contradict intent |
| Comparatives | *"Worse than the last one"* | Sentiment relative, not absolute |
| Domain reinterpretation | *"This bond is sick"* (finance) | Word polarity inverts by domain |
| Conditional / hypothetical | *"If only it were good"* | Modality flips evaluation |
| Aspect grouping | *"Great camera, awful battery"* | Document score averages opposites |

> [!warning] Common Misconception
> Adding more negation rules does not fix this — every patch reveals a deeper composition problem. The structural answer is to abandon pure lexical aggregation and use models (Naïve Bayes, logistic regression, neural) that learn from labelled data how words interact.

## Significance

This is the limit of count-based sentiment modelling, exactly parallel to the limit reached in [[Word Embeddings]]: meaning is compositional, but Bag-of-Words representations cannot express composition. Recognising this failure motivates the move from lexicons to learned classifiers, and ultimately to context-sensitive embeddings.
