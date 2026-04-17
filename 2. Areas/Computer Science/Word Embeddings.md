**Tags:** #hub #nlp #embeddings
**Related:** [[Natural Language Processing]], [[Embeddings]], [[Distributional Hypothesis]]

## Overview

Word embeddings are dense, low-dimensional vector representations of words learned from large corpora. Unlike sparse count-based vectors, embeddings capture semantic and syntactic regularities as geometric relationships in vector space — enabling analogy arithmetic and semantic similarity queries.

> [!abstract]- TL;DR
> Word embeddings compress distributional statistics into dense vectors where similar words cluster together. Word2Vec, GloVe, and fastText each learn these vectors differently but all exploit the distributional hypothesis: a word is defined by the company it keeps.

## Knowledge Map

### 1. Prediction-Based Models
- [[Word2Vec]]
- [[CBOW vs Skip-gram]]

### 2. Count-Based Models
- [[GloVe]]

### 3. Subword Models
- [[fastText]]

### 4. Evaluation
- [[Intrinsic vs Extrinsic Evaluation of Embeddings]]

> [!question]- Common Exam Questions
> - What is the difference between CBOW and Skip-gram in Word2Vec?
> - How does GloVe combine global co-occurrence statistics with local context?
> - Why does fastText handle OOV words better than Word2Vec?
> - What is the analogy test and what does passing it imply about an embedding space?
