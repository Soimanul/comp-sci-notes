**Tags:** #concept #llm
**Related:** [[Flash Attention]], [[Transformer Architecture]]

## Definition

**Kernel fusion** is a GPU optimisation technique that combines multiple sequential GPU operations (kernels) into a single kernel, eliminating the overhead of reading/writing intermediate results to GPU memory (HBM) between operations.

> [!info] Key Intuition
> Each GPU operation (ReLU, add, layer norm) is a separate "kernel launch" that reads from global GPU memory and writes back. For small operations, the memory bandwidth cost dominates the compute cost. Fusing them into one kernel keeps data in fast on-chip SRAM, dramatically reducing memory traffic.

## GPU Memory Hierarchy

| Memory | Capacity | Bandwidth | Latency |
|---|---|---|---|
| HBM (VRAM) | 40–80 GB | ~2 TB/s | High |
| L2 Cache | Few MB | ~10 TB/s | Medium |
| SRAM (on-chip) | Few MB | ~20 TB/s | Very low |

For memory-bound operations (small matrices, element-wise ops), HBM bandwidth is the bottleneck — not compute.

## Example: Fused Attention

**Without fusion (naïve):**
1. Compute $QK^T$ → write to HBM
2. Scale by $\sqrt{d_k}$ → write to HBM
3. Softmax → write to HBM
4. Multiply by $V$ → write to HBM

4 HBM reads/writes per attention block.

**With fusion** ([[Flash Attention]]):
Entire attention computation in one kernel using tiling in SRAM — only read $Q, K, V$ once and write output once.

## Common Fused Operations in LLMs

| Fused Op | Components |
|---|---|
| Fused LayerNorm | Mean, variance, normalise, scale, shift |
| Fused attention | Q×K, scale, mask, softmax, ×V |
| Fused activation | GeLU/SiLU + linear |
| Fused residual + norm | Add + LayerNorm |

## Significance

Kernel fusion is one of the primary tools in high-performance LLM inference frameworks (TensorRT, vLLM, FlashInfer). It can reduce memory bandwidth usage by 2–10× for fused ops, translating directly to higher throughput and lower latency.
