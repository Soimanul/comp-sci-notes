**Tags:** #concept #dl #nlp
**Related:** [[Transformer Architecture]], [[Self-Attention]], [[Multi-Head Self-Attention]]

## Definition

The **attention mechanism** is a neural network operation that computes a weighted sum of a set of **values** $V$, where the weights are determined by the compatibility (similarity) between a set of **queries** $Q$ and **keys** $K$.

> [!info] Key Intuition
> "Pay attention to the most relevant things." Given a query (what I'm looking for) and a set of key-value pairs (what's available), the attention mechanism scores how well each key matches the query and returns a weighted combination of the corresponding values.

## Scaled Dot-Product Attention

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

Where:
- $Q \in \mathbb{R}^{n \times d_k}$ — queries (one per output position)
- $K \in \mathbb{R}^{m \times d_k}$ — keys (one per input position)
- $V \in \mathbb{R}^{m \times d_v}$ — values (one per input position)
- $\frac{1}{\sqrt{d_k}}$ — scaling factor to prevent gradient saturation

## Step by Step

1. Compute raw scores: $S = QK^T$ — shape $(n \times m)$
2. Scale: $S / \sqrt{d_k}$
3. Apply softmax: $\alpha = \text{softmax}(S / \sqrt{d_k})$ — attention weights, each row sums to 1
4. Weighted sum: $\text{output} = \alpha V$

## Why Scale by $\sqrt{d_k}$?

For large $d_k$, dot products grow in magnitude, pushing softmax into near-zero gradient regions. Dividing by $\sqrt{d_k}$ keeps the variance of dot products at ~1 regardless of dimensionality.

> [!example]- Retrieval Analogy
> Query: "What did the meeting decide about budget?"
> Keys: sentence topics ["budget approval", "meeting time", "next agenda"]
> The attention weights heavily on "budget approval" → the output is a blend of values dominated by the budget-related content.

## Variants

| Variant | Description |
|---|---|
| Self-attention | Q, K, V all come from the same sequence |
| Cross-attention | Q from one sequence; K, V from another (encoder-decoder) |
| Masked attention | Set future positions' scores to $-\infty$ before softmax |
| Multi-head | Run multiple attention heads in parallel, concat outputs |

## Significance

Attention is the core operation of the Transformer and has replaced RNNs as the dominant sequence modelling mechanism in NLP, vision, and multimodal systems.
