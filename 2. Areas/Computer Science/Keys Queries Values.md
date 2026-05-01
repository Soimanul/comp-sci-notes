**Tags:** #concept #nlp #neural-networks
**Related:** [[Attention Mechanism]], [[Self-Attention]], [[Bahdanau Attention]]

## Definition
The attention mechanism is most naturally framed as a soft, differentiable lookup in a key–value store:
- **Queries** $Q$ — what we are looking up.
- **Keys** $K$ — labels indexing the items.
- **Values** $V$ — the items themselves to be returned.

The output is a weighted combination of the values, with weights determined by the similarity between each query and each key:
$$\mathrm{Attention}(Q, K, V) = \mathrm{softmax}\!\left(\frac{QK^\top}{\sqrt{d_k}}\right) V$$

> [!info] Key Intuition
> Attention is a learned database lookup. Each query asks "what's relevant to me?", keys advertise what each position has, and the answer is a smooth blend of all values weighted by relevance.

## Where Each Comes From

| Setting | Queries $Q$ | Keys $K$ | Values $V$ |
|---|---|---|---|
| Bahdanau encoder–decoder | Decoder hidden state $s_t$ | Encoder hidden states $h_i$ | Encoder hidden states $h_i$ |
| Encoder self-attention | Encoder token rep | Encoder token rep | Encoder token rep |
| Decoder self-attention | Decoder token rep | Decoder token rep | Decoder token rep |
| Encoder–decoder cross-attention | Decoder token rep | Encoder output | Encoder output |

Each is a learned projection: $Q = X W^Q$, $K = X W^K$, $V = X W^V$ — for self-attention $X$ is the same sequence; for cross-attention $X$ differs between $Q$ and $(K,V)$.

> [!warning] Common Misconception
> Keys and values are *not* the same vectors in general — they are produced by *different* learned projection matrices, even when they come from the same source sequence. Tying them sometimes works for efficiency but loses expressiveness.

## Significance
The Q/K/V abstraction is the lingua franca of modern attention. Once a model is described in those terms, all the variants — self, cross, masked, multi-head, sparse — are just choices about where each tensor comes from and what mask is applied.
