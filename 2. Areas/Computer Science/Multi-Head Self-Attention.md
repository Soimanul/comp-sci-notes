**Tags:** #concept #dl #nlp
**Related:** [[Self-Attention]], [[Attention Mechanism]], [[Transformer Architecture]]

## Definition

**Multi-head self-attention** runs $h$ self-attention operations (**heads**) in parallel, each with its own projection matrices, then concatenates and projects their outputs. This allows the model to jointly attend to information from different representation subspaces at different positions.

> [!info] Key Intuition
> A single attention head can only focus on one type of relationship at a time. Multiple heads can simultaneously capture: syntactic dependencies, coreference, semantic similarity, and positional proximity — each head specialising in a different aspect of the relationship structure.

## Equations

**Per head $i$:**
$$\text{head}_i = \text{Attention}(QW_i^Q,\ KW_i^K,\ VW_i^V)$$

where $W_i^Q, W_i^K \in \mathbb{R}^{d_{model} \times d_k}$ and $W_i^V \in \mathbb{R}^{d_{model} \times d_v}$, with $d_k = d_v = d_{model}/h$.

**Concatenation + projection:**
$$\text{MultiHead}(Q, K, V) = \text{Concat}(\text{head}_1, \ldots, \text{head}_h) W^O$$

where $W^O \in \mathbb{R}^{hd_v \times d_{model}}$.

## Dimensions (BERT-base)

| Hyperparameter | Value |
|---|---|
| $d_{model}$ | 768 |
| $h$ (heads) | 12 |
| $d_k = d_v = d_{model}/h$ | 64 |

## Why Multiple Heads?

Each head learns different $W^Q, W^K, W^V$ projections → different attention patterns:
- Head 1 might attend to the syntactic subject
- Head 2 might attend to the nearest noun
- Head 3 might attend to coreferences

Empirical visualisation (Vig 2019) confirms heads specialise in interpretable linguistic patterns.

## Computational Cost

Total cost ≈ same as one head with dimension $d_{model}$ (due to reduced per-head dimension). No additional FLOPs vs. single-head attention of the same total dimension — but significantly more expressive.

> [!warning] Too Many Heads
> Beyond a certain number of heads, performance plateaus or degrades (heads become redundant). Optimal head count is a hyperparameter typically set to 8 or 12 for standard Transformer models.

## Significance

Multi-head attention is the key architectural innovation that allows Transformers to model multiple types of linguistic relationships simultaneously, which is critical for the deep contextual representations used in BERT and GPT models.
