**Tags:** #concept #nlp #embeddings
**Related:** [[Skip-Gram Objective]], [[Negative Sampling]], [[Latent Semantic Analysis (LSA)]]

## Definition

Levy & Goldberg (2014) showed that **Skip-Gram with Negative Sampling (SGNS)** implicitly factorises a **shifted Pointwise Mutual Information** matrix. Under suitable assumptions, the learned dot product between a word vector and a context vector approximates

$$v_w^{\top} u_c \approx \text{PMI}(w, c) - \log k,$$

where

$$\text{PMI}(w, c) = \log \frac{P(w, c)}{P(w) P(c)}$$

and $k$ is the number of negative samples per positive pair.

> [!info] Key Intuition
> Word2Vec is not a fundamentally new object — it is **matrix factorisation in disguise**. The difference from LSA is *how* the factorisation is performed: implicitly via gradient descent rather than explicitly via SVD on a fixed matrix.

## The Required Assumptions

The equivalence holds when:

- the corpus is large,
- contexts are independent,
- the embedding dimension $d$ is sufficiently large,
- the negative sampling distribution matches the unigram distribution,
- the optimisation reaches a global optimum.

In practice these are approximated; embeddings empirically behave as if they encode shifted PMI.

## Why This Matters

| Method | Matrix factorised | How |
|---|---|---|
| LSA | Term–document or term–term counts | Explicit truncated SVD |
| GloVe | log of co-occurrence ratios | Weighted least squares |
| Word2Vec (SGNS) | Shifted PMI | Implicit, via SGD on local objectives |

The predictive route scales better because:

- it processes one local window at a time (no global matrix in memory);
- it adapts naturally to streaming corpora;
- it produces flexible representations that respond to fine-grained training-set choices (windows, subsampling, noise distribution).

> [!warning] Common Misconception
> "Embeddings are deep" — they are not. Word2Vec is a **single-layer** linear model. The non-trivial behaviour comes from the choice of objective and the size of the data, not from depth or non-linearity.

## Significance

This result reconciled two seemingly opposed traditions: the count-based decomposition lineage (LSA, HAL, GloVe) and the predictive lineage (Word2Vec). It also clarified that the magic of word embeddings is not in *predicting* per se but in **factorising co-occurrence statistics in a smooth low-dimensional space** — the same goal LSA pursued, accomplished via a more scalable optimisation.
