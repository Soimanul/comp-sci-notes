**Tags:** #concept #dl #nlp
**Related:** [[Attention Mechanism]], [[Multi-Head Self-Attention]], [[Transformer Architecture]]

## Definition

**Self-attention** is an attention operation where the queries, keys, and values all come from the **same sequence** — each token attends to all other tokens in the same sequence to build a contextualised representation.

> [!info] Key Intuition
> In the sentence "The animal didn't cross the street because **it** was too tired," self-attention allows "it" to look at all other words and determine that "it" refers to "animal" (not "street"). Each token's final representation incorporates information from the tokens it most attends to.

## Mechanism

Given an input sequence $X \in \mathbb{R}^{n \times d}$:

1. Project to queries, keys, values:
$$Q = XW^Q, \quad K = XW^K, \quad V = XW^V$$
where $W^Q, W^K \in \mathbb{R}^{d \times d_k}$ and $W^V \in \mathbb{R}^{d \times d_v}$ are learned projection matrices.

2. Compute attention:
$$\text{SelfAttn}(X) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

3. Output: each position's new representation is a weighted sum of all positions' value vectors.

## Attention Pattern Example

```
The  animal  didn't  cross  because  it  was  tired
 ↑      ↑↑↑    ↑       ↑      ↑       ↑   ↑
High attention from "it" to "animal"
```

## Key Properties

| Property | Description |
|---|---|
| Permutation equivariant | Swapping input positions swaps output positions; positional encoding is needed |
| Global receptive field | Every token can directly attend to every other token (no distance decay) |
| Quadratic complexity | $O(n^2 d)$ in sequence length $n$ |
| Fully parallel | All attention weights computed simultaneously (unlike RNN's sequential processing) |

## Bidirectional vs. Unidirectional

- **Bidirectional** (BERT encoder): each token attends to all tokens — full context
- **Unidirectional/Causal** (GPT decoder): each token attends only to previous tokens — left context only

## Significance

Self-attention is the fundamental operation that enables Transformers to build deeply contextualised representations, replacing the sequential hidden states of RNNs with a direct, parallel, global interaction mechanism.
