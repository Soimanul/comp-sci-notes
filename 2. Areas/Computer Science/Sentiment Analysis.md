**Tags:** #hub #nlp #sentiment
**Related:** [[Natural Language Processing]], [[Naïve Bayes]], [[Logistic Regression]]

## Overview

Sentiment Analysis (Opinion Mining) is the computational study of opinions, sentiments, emotions, and appraisals expressed in text toward an entity or one of its features. It ranges from coarse-grained document-level polarity classification to fine-grained aspect-level analysis, and extends to **sentiment trajectories** that treat tone as a temporal signal across discourse.

> [!abstract]- TL;DR
> An opinion is formally a quintuple $(e, a, s, h, t)$. Most practical systems collapse it to a single polarity label $s$ and predict it with three competing perspectives — n-gram language models, Naïve Bayes, or logistic regression — or aggregate lexicon scores. Beyond static classification, sentiment can be tracked sentence-by-sentence to expose discourse and rhetorical structure.

## Knowledge Map

### 1. What Sentiment Is
- [[Opinion Mining]]
- [[Subjectivity vs Objectivity in Text]]
- [[Sentiment Triple]]
- [[Opinion Quintuple]]

### 2. Lexicon-Based Approaches
- [[Sentiment Lexicons]]
- [[Lexicon Scoring]]
- [[Compositional Challenges in Lexicon Scoring]]
- [[VADER]]

### 3. Three Perspectives on Sentiment Classification
- [[Three Perspectives on Sentiment Classification]]
- [[Naïve Bayes]]
- [[Logistic Regression]]

### 4. Sentiment Beyond Documents
- [[Aspect-Based Sentiment Analysis]]
- [[Sentiment as Temporal Signal]]

> [!question]- Common Exam Questions
> - Write down the opinion quintuple and explain each component.
> - What is the difference between an opinion, a sentiment, and an emotion?
> - State the lexicon-based scoring formula and explain how negation breaks it.
> - Compare the n-gram, Naïve Bayes, and logistic regression formulations of sentiment classification — what does each fundamentally ask?
> - How does treating sentiment as a temporal signal change what the analysis reveals?
> - Why is the Loughran–McDonald lexicon needed for financial text?
