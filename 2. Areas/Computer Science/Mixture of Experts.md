**Tags:** #concept #llm
**Related:** [[Transformer Architecture]], [[KV Caching]], [[ZeRO Optimizer]]

## Definition

**Mixture of Experts (MoE)** is a model architecture where the feed-forward layers are replaced by a collection of **expert** sub-networks, with a **router** that selects a small subset of experts (typically 2 of $N$) to process each token — enabling a much larger total parameter count while keeping per-token compute constant.

> [!info] Key Intuition
> A 70B dense model uses all 70B parameters for every token. A 141B MoE model routes each token through only 2 of 8 experts (≈ 2×7B = 14B active parameters per token). The model capacity is 141B but the compute is 14B — you get large-model expressiveness at small-model cost.

## Architecture

**Standard Transformer FFN:**
$$\text{FFN}(x) = W_2 \cdot \text{ReLU}(W_1 x + b_1) + b_2$$

**MoE FFN replacement:**
$$\text{MoE-FFN}(x) = \sum_{i=1}^{k} g_i(x) \cdot E_i(x)$$

where:
- $E_i(x)$ = expert $i$'s FFN output
- $g_i(x)$ = router gate for expert $i$ (top-$k$ softmax)
- Only $k$ experts (typically $k=2$) are active per token

## Router

$$g(x) = \text{Softmax}(\text{TopK}(x \cdot W_g))$$

The router is a linear layer learned jointly with the experts. Only the top-$k$ gate values are kept; the rest are zeroed out.

## Load Balancing

Without regularisation, the router may over-use a few experts. An **auxiliary load balancing loss** encourages each expert to receive a roughly equal fraction of tokens:

$$L_{aux} = \alpha \cdot N \sum_{i=1}^{N} f_i \cdot P_i$$

where $f_i$ = fraction of tokens routed to expert $i$ and $P_i$ = average router probability for expert $i$.

## Notable MoE Models

| Model | Total params | Active params | Experts |
|---|---|---|---|
| Mixtral 8x7B | 46.7B | 12.9B | 8 experts, top-2 |
| GPT-4 (rumoured) | ~1.8T | ~110B | 16 experts |
| Gemini 1.5 | ~1T | — | MoE (undisclosed) |

## Significance

MoE enables training models with dramatically more parameters than compute-equivalent dense models, improving capability without proportional cost. It is the architecture behind several of the best-performing LLMs (Mixtral, rumoured GPT-4).
