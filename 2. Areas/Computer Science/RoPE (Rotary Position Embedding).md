**Tags:** #concept #llm
**Related:** [[Positional Encoding]], [[Transformer Architecture]], [[KV Caching]]

## Definition

**RoPE (Rotary Position Embedding)** is a positional encoding scheme that encodes absolute position by applying a rotation to the query and key vectors in attention, with the rotation angle dependent on the token's position — enabling the attention dot product to naturally capture **relative** position distances.

> [!info] Key Intuition
> Standard learned positional embeddings are added to token embeddings — crude and fixed at training length. RoPE multiplies queries and keys by a rotation matrix, so the dot product $q_m^T k_n$ depends only on the relative position $(m - n)$. This is more elegant and generalises better to longer sequences than training length.

## Mechanism

For a query at position $m$ and key at position $n$, RoPE rotates the 2D sub-vectors of $q$ and $k$ by angles proportional to position:

$$q_m = R_m q, \quad k_n = R_n k$$

$$q_m^T k_n = (R_m q)^T (R_n k) = q^T R_m^T R_n k = q^T R_{m-n} k$$

The inner product depends only on the **relative position** $m - n$, which is exactly the bias we want in attention.

## Rotation Matrix

For pair of dimensions $(2i, 2i+1)$ at position $pos$:

$$R_{pos}^{(i)} = \begin{pmatrix} \cos(pos \cdot \theta_i) & -\sin(pos \cdot \theta_i) \\ \sin(pos \cdot \theta_i) & \cos(pos \cdot \theta_i) \end{pmatrix}$$

where $\theta_i = 10000^{-2i/d}$ (same base as sinusoidal encoding).

## RoPE vs. Other Positional Encodings

| Type | Relative positions | Extrapolation | Used in |
|---|---|---|---|
| Sinusoidal (fixed) | No | Good | Original Transformer |
| Learned (BERT/GPT) | No | Poor (can't extrapolate) | BERT, GPT-2 |
| **RoPE** | Yes (naturally) | Good (with scaling) | LLaMA, Mistral, GPT-NeoX |
| ALiBi | Yes (bias) | Excellent | BLOOM, MPT |

## Context Extension

RoPE can be extended to handle sequences longer than training length via **RoPE scaling** (scaling the base $\theta$ or interpolating positions) — used in models like LLaMA with extended context windows.

## Significance

RoPE is now the dominant positional encoding in modern open-source LLMs (LLaMA, Mistral, Qwen). Its relative-position property improves attention for long contexts, and its compatibility with KV caching (no additional overhead) makes it ideal for production deployment.
