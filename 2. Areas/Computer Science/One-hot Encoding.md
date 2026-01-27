**Tags:** #concept #nlp #representation #sparse-vectors  
**Related:** [[Sparse Representations]] · [[Bag-of-Words (BoW)]] · [[Term–Document Matrix]] · [[Vector Space Model (VSM)]]

## Definition
**One-hot encoding** represents each token as a vector of length |V| (vocabulary size) with a single 1 at the index of the token and 0 elsewhere.

## What it represents
- A one-hot vector is a **categorical identity representation**:
  - it encodes *which word it is*,
  - but encodes no similarity between words.

## Properties
- **High-dimensional and sparse**: exactly one non-zero entry.
- **Orthogonal basis**: different tokens have dot product 0.
- **No semantic structure**: all distinct tokens are equally dissimilar in this representation.

## How it composes into larger representations
- A sequence (sentence/document) can be seen as:
  - a sequence of one-hot vectors, or
  - an aggregate of them (e.g., summed counts → Bag-of-Words).

## Why it still matters
- It is the conceptual base of sparse NLP representations and helps explain:
  - how Bag-of-Words arises from aggregating token identities,
  - why TF–IDF is a reweighting of the same feature space,
  - why dense embeddings can be viewed as a learned transformation from token identities into a lower-dimensional space.

## Limitations
- Vocabulary growth increases dimensionality linearly.
- Captures neither synonymy (different words, similar meaning) nor polysemy (same word, multiple senses).
- Inefficient for similarity search without additional structure (weighting, factorization, or learned embeddings).
