**Tags:** #hub #nlp #topic-modelling
**Related:** [[Natural Language Processing]], [[Vector Space Model (VSM)]], [[Latent Semantic Analysis (LSA)]]

## Overview

Topic modelling shifts NLP from **geometric** representation (counts, vectors, matrix factorisation) to **generative probabilistic** modelling. Instead of asking "what linear structure best approximates the data?", topic models ask "what hidden thematic components could have generated the observed word counts?"

> [!abstract]- TL;DR
> Vector space models and LSA describe how documents are positioned, not how they are produced. Topic models like LDA posit hidden topics as probability distributions over words, with each document as a mixture of topics. The Dirichlet distribution provides the conjugate prior over those mixture vectors.

## Knowledge Map

### 1. Why VSM and LSA Are Not Enough
- [[Vector Space Model (VSM)]]
- [[Latent Semantic Analysis (LSA)]]
- [[Limits of LSA]]

### 2. Probability Foundations
- [[Beta Distribution]]
- [[Dirichlet Distribution]]
- [[Dirichlet–Multinomial Conjugacy]]

### 3. The Generative Topic Model
- [[Latent Dirichlet Allocation (LDA)]]
- [[LSA vs LDA]]

> [!question]- Common Exam Questions
> - Why does LSA fail to qualify as a generative model?
> - State the Dirichlet density and explain what its hyperparameters $\alpha_k$ control.
> - Write the LDA generative process for a single document.
> - Compare LSA and LDA: what is "latent" in each?
> - What does it mean to say the Dirichlet is the conjugate prior of the Multinomial?
