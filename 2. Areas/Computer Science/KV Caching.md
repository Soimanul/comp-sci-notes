**Tags:** #concept #llm
**Related:** [[Transformer Architecture]], [[Paged Attention]], [[Multi-Query and Grouped-Query Attention]]

## Definition

**KV Caching** is an inference optimisation that stores the key and value tensors from the attention mechanism for all previously processed tokens, avoiding their recomputation on each new generation step during autoregressive decoding.

> [!info] Key Intuition
> In autoregressive generation, at step $t$ the model processes tokens $[1, \ldots, t-1, t]$ to predict token $t+1$. Tokens $1, \ldots, t-1$ were processed at every previous step. KV caching stores their $K$ and $V$ tensors after the first computation — subsequent steps only compute $K, V$ for the new token $t$.

## Why Keys and Values?

In self-attention: $\text{Attention}(Q, K, V)$

- At step $t$, the **query** $q_t$ is new (only depends on token $t$)
- The **keys** $K_{1:t-1}$ and **values** $V_{1:t-1}$ from past tokens are **unchanged**
- Cache $K_{1:t-1}$ and $V_{1:t-1}$ and append $k_t, v_t$ at each step

## Memory Cost

For a model with $L$ layers, $H$ heads, head dimension $d$, sequence length $T$, batch size $B$:

$$\text{KV cache size} = 2 \times L \times H \times d \times T \times B \times \text{dtype bytes}$$

For LLaMA-2-70B with batch=1, T=4096 tokens: ≈ 8GB — a significant fraction of GPU memory.

## Compute Savings

Without KV cache: compute scales as $O(T^2)$ per generated token (must reprocess all previous tokens).
With KV cache: compute scales as $O(T)$ per generated token — orders of magnitude faster.

## Limitations

- **Memory**: large KV caches limit batch size; memory fragmentation is a problem ([[Paged Attention]])
- **Context length**: KV cache grows linearly with context; very long contexts exhaust GPU memory
- **Static allocation**: naïve implementations pre-allocate max-length KV cache, wasting memory for short sequences

## Significance

KV caching is the most important single inference optimisation for Transformer-based LLMs. Without it, serving GPT-4-class models at production throughput would be infeasible.
