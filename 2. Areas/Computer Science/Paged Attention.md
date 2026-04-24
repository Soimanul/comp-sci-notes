**Tags:** #concept #llm
**Related:** [[KV Caching]], [[Transformer Architecture]]

## Definition

**Paged Attention** is a memory management technique for LLM inference that stores KV cache tensors in non-contiguous **pages** (fixed-size blocks) inspired by virtual memory in operating systems, eliminating internal fragmentation and enabling much higher GPU utilisation.

> [!info] Key Intuition
> Naïve KV caching pre-allocates a contiguous chunk of GPU memory equal to the maximum possible sequence length. Most of this memory is wasted for short sequences, and reallocation for sequences that grow is expensive. Paged Attention allocates memory in small pages on demand — like virtual memory pages — dramatically improving utilisation.

## The Memory Fragmentation Problem

**Without paged attention:**
- Allocate a contiguous block of size `max_len × hidden_dim` per sequence at request start
- If max_len = 2048 but actual length = 100: 95% of allocated memory is wasted
- Different requests can't share memory even if pages are free

**With paged attention:**
- KV cache is divided into fixed-size **pages** (e.g. 16 tokens per page)
- A **page table** maps logical token positions to physical page locations
- New pages allocated only as tokens are generated
- Pages freed immediately when a sequence finishes

## Block Manager

The **block manager** maintains:
- A pool of free physical pages
- A per-sequence logical→physical page table
- Handles allocation, deallocation, and copy-on-write (for beam search)

## Benefits

| Benefit | Description |
|---|---|
| Near-zero wasted memory | Only allocate what is needed |
| Higher batch sizes | More sequences fit on the same GPU |
| Copy-on-write for beam search | Beam candidates share prefixes without copying until they diverge |
| Memory pooling | Pages from finished requests immediately available for new ones |

## vLLM

Paged Attention was introduced by **vLLM** (Kwon et al., 2023), which achieved 2–4× higher throughput than Hugging Face Transformers by virtually eliminating memory waste.

## Significance

Paged Attention is now the standard memory management approach for production LLM serving systems. vLLM, TGI (HuggingFace), and TensorRT-LLM all implement variants of this approach.
