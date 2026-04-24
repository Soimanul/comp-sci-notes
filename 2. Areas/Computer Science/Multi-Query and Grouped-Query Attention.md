**Tags:** #concept #llm
**Related:** [[Multi-Head Self-Attention]], [[KV Caching]], [[Transformer Architecture]]

## Definition

**Multi-Query Attention (MQA)** shares a single set of key-value heads across all query heads, dramatically reducing the KV cache memory footprint. **Grouped-Query Attention (GQA)** is a middle ground: it groups query heads into $G$ groups, each sharing one K/V head.

> [!info] Key Intuition
> In standard multi-head attention (MHA), each of $H$ heads has its own K and V matrices. At inference, all $H$ sets of K, V tensors must be cached. MQA reduces this to 1 set (extreme sharing). GQA uses $G$ sets ($1 \leq G \leq H$) — trading some quality for large memory savings.

## Variants

### Multi-Head Attention (MHA)
- $H$ query heads, $H$ key heads, $H$ value heads
- KV cache: $2 \times H \times d_v$ per token
- Best quality; highest memory

### Multi-Query Attention (MQA)
- $H$ query heads, **1 key head, 1 value head**
- KV cache: $2 \times 1 \times d_v$ per token — $H\times$ reduction
- Slightly lower quality than MHA
- Used in: PaLM, Falcon, early Gemini

### Grouped-Query Attention (GQA)
- $H$ query heads, **$G$ key heads, $G$ value heads** (groups of $H/G$ query heads per KV head)
- KV cache: $2 \times G \times d_v$ per token — $H/G \times$ reduction
- Quality close to MHA; memory close to MQA
- Used in: LLaMA 2 70B, LLaMA 3, Mistral, Gemma

## Comparison

| Method | Query heads | KV heads | KV cache | Quality |
|---|---|---|---|---|
| MHA | $H$ | $H$ | $H \times$ base | Best |
| GQA ($G=H/4$) | $H$ | $H/4$ | $H/4 \times$ base | Very close to MHA |
| MQA ($G=1$) | $H$ | $1$ | $1 \times$ base | Slightly worse |

> [!example]- LLaMA 3 8B Configuration
> $H = 32$ query heads, $G = 8$ KV heads.
> KV cache = $8/32 = 25\%$ of MHA — 4× memory reduction with minimal quality loss.

## Converting MHA → GQA

Existing MHA models can be converted to GQA by **mean pooling** the K/V heads within each group — then fine-tune on a small dataset to recover quality (Ainslie et al., 2023).

## Significance

GQA is now the standard attention variant in new LLM releases (LLaMA 2+, Mistral, Gemma) because it maintains MHA quality while reducing KV cache by 4–8×, enabling larger batch sizes and longer context windows at the same GPU memory budget.
