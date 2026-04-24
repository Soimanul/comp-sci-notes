**Tags:** #concept #llm #dl
**Related:** [[Kernel Fusion]], [[Transformer Architecture]], [[Multi-Head Self-Attention]], [[KV Caching]]

## Definition

**Flash Attention** is an IO-aware exact attention algorithm that reorders the attention computation to tile it across SRAM (on-chip memory), reducing HBM memory reads/writes from $O(N^2)$ to $O(N)$, achieving 2–4× speed-up over standard attention without approximation.

> [!info] Key Intuition
> Standard attention computes the full $N \times N$ attention matrix and writes it to HBM. For N = 4096, this is 64M floats per layer — a huge memory bottleneck. Flash Attention avoids materialising this matrix entirely, computing the output in small tiles that fit in SRAM.

## Standard Attention Memory Cost

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right) V$$

1. Compute $S = QK^T$ — shape $(N \times N)$, write to HBM: $O(N^2)$
2. Compute $P = \text{softmax}(S)$ — shape $(N \times N)$, write to HBM: $O(N^2)$
3. Compute $O = PV$ — shape $(N \times d)$

Total HBM writes: $O(N^2)$ — the bottleneck for long sequences.

## Flash Attention Algorithm

Uses **tiling**: partition $Q, K, V$ into blocks that fit in SRAM. For each block of $K, V$:
1. Load block into SRAM
2. Compute partial dot products with $Q$
3. Apply online softmax (numerically stable running max and sum)
4. Accumulate partial output
5. Discard intermediate $S, P$ — never write to HBM

**HBM reads/writes:** $O(N \cdot d)$ — linear in $N$.

## Online Softmax

To compute softmax correctly without materialising the full row, Flash Attention uses the **softmax rescaling trick**:
- Maintain running maximum $m$ and running sum $\ell$
- As new tiles arrive, rescale previously accumulated output

## Flash Attention 2 / 3

| Version | Key improvement |
|---|---|
| FA-1 | Original tiling; 2–4× speedup over standard |
| FA-2 | Better work partitioning; 2× speedup over FA-1 |
| FA-3 | Async pipelines for H100 Tensor Cores; further speedup |

## Significance

Flash Attention enabled training Transformers with sequences 4–8× longer than previously feasible and halved training time for large models. It is now the default attention implementation in virtually all production training frameworks (PyTorch 2.0 built it in).
