**Tags:** #concept #reco #dl
**Related:** [[Sequential vs Session-Based Recommendation]], [[Transformer Architecture]], [[Self-Attention]], [[GRU for Recommendations]]

## Definition

**Transformer for Sequential Recommendations (SASRec)** applies the Transformer encoder with **unidirectional (causal) self-attention** to model sequential user interactions. Each item attends to all previous items in the sequence, identifying which past interactions most influence the next item prediction.

> [!info] Key Intuition
> Unlike RNNs that compress all history into one vector, the Transformer attends to the most relevant past interactions directly. For a user who has been browsing laptops, self-attention will learn to focus on the laptop-related items regardless of when they occurred in the history.

## SASRec Architecture

**Input:** sequence of item embeddings $e_1, e_2, \ldots, e_t$ + positional embeddings

**Each layer (Transformer block):**
1. **Masked multi-head self-attention**: item $i$ attends to items $1, \ldots, i-1$ only (causal masking)
2. **Point-wise feed-forward network**: 2-layer MLP applied independently per position
3. **Residual connection + layer norm** around each sub-layer

**Prediction:** use the output representation at the last position $h_t$ to score all candidate items:
$$\hat{r}_{u,i} = h_t^T q_i$$

## Causal Masking

SASRec uses a **lower triangular attention mask** to prevent each position from attending to future positions:

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}} + M\right)V$$

where $M_{ij} = -\infty$ if $j > i$, 0 otherwise.

## SASRec vs. BERT4Rec

| Property | SASRec | BERT4Rec |
|---|---|---|
| Attention direction | Unidirectional (causal) | Bidirectional |
| Training task | Next item prediction | Masked item prediction (Cloze) |
| Inference | Sequential | Requires masking the target |
| Speed | Faster at inference | More expressive |

> [!warning] Sequence Length
> Transformers scale quadratically with sequence length (attention matrix is $T \times T$). For very long histories, truncation or sparse attention is needed.

## Significance

SASRec (Kang & McAuley, 2018) consistently outperforms RNN and CNN sequential models and is the standard Transformer baseline for sequential recommendation. BERT4Rec extends it with bidirectional attention for better representation learning.
