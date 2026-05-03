**Tags:** #hub #nlp #embeddings
**Related:** [[Natural Language Processing]], [[Vector Space Model (VSM)]], [[Distributional Hypothesis]], [[Latent Dirichlet Allocation (LDA)]]

## Overview

Word embeddings replace **count-based** word representations with **dense, learned** vectors. Where Bag-of-Words, TF–IDF, LSA, and LDA all treat the word as an atomic symbol whose meaning is reconstructed indirectly from co-occurrence statistics, embeddings define meaning as a parameter learned by minimising prediction error. The geometry of the embedding space is intrinsic — similarity is encoded in vector inner products, not in shared counts.

> [!abstract]- TL;DR
> Classical distribution collapses under sparsity, synonymy, polysemy, order loss, and compositional interactions. Word2Vec replaces it with the predictive paradigm: each word becomes a learnable vector in $\mathbb{R}^d$, trained so that similar contexts produce similar predictions. Skip-Gram with negative sampling is implicitly factorising a shifted PMI matrix — predictive and count-based methods are not unrelated, but the predictive route scales and generalises better.

## Knowledge Map

### 1. Why Classical Distribution Collapses
- [[Limits of Count-Based Representations]]

### 2. The Predictive Turn
- [[Word2Vec]]
- [[CBOW vs Skip-gram]]
- [[Skip-Gram Objective]]
- [[Negative Sampling]]

### 3. Connections and Interpretation
- [[Word2Vec PMI Equivalence]]
- [[Embedding Geometry and Analogies]]

### 4. Other Embedding Families
- [[GloVe]]
- [[fastText]]

### 5. Evaluation and Limits
- [[Intrinsic vs Extrinsic Evaluation of Embeddings]]
- [[Static Embedding Limits]]

> [!question]- Common Exam Questions
> - Name three structural failures of Bag-of-Words that motivate dense embeddings.
> - Write the Skip-Gram softmax objective and explain why the denominator is computationally prohibitive.
> - State the negative sampling objective. What does it approximate and how?
> - Under what assumptions does Skip-Gram with negative sampling factorise a shifted PMI matrix?
> - Why do static embeddings fail to handle polysemy, and how do contextual models address it?
> - Explain the king − man + woman ≈ queen result geometrically.
