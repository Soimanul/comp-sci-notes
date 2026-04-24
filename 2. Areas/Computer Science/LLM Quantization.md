**Tags:** #concept #llm
**Related:** [[QLoRA]], [[Mixed Precision Training]], [[Speculative Decoding]]

## Definition

**LLM Quantization** is the process of reducing the numerical precision of model weights and/or activations from FP16/BF16 to lower bit widths (INT8, INT4, INT3, INT2), reducing memory footprint and increasing inference throughput at the cost of some model quality.

> [!info] Key Intuition
> FP16 uses 2 bytes per parameter; INT4 uses 0.5 bytes. A 7B parameter model in FP16 requires 14 GB; in INT4 it requires ~3.5 GB — fits on a laptop GPU. The challenge is mapping the continuous weight values to a small discrete set without too much quality loss.

## Quantization Basics

**Uniform quantization** of a weight $w$:
$$w_q = \text{round}\left(\frac{w - \text{min}}{(\text{max} - \text{min}) / (2^b - 1)}\right)$$
$$w_{\text{dequant}} = w_q \cdot \frac{\text{max} - \text{min}}{2^b - 1} + \text{min}$$

## When to Quantize

| Technique | When Applied | Notes |
|---|---|---|
| **Post-Training Quantization (PTQ)** | After training, no gradient updates | Fast; small quality drop at INT8; larger at INT4 |
| **Quantization-Aware Training (QAT)** | During training with simulated quant | Better quality; requires full retraining |

## Granularity

| Level | Description | Quality |
|---|---|---|
| Per-tensor | One scale for all weights | Lowest quality |
| Per-channel | One scale per output channel | Better |
| Per-group | One scale per block of $g$ weights | Best (most common in INT4) |

## Key Methods

| Method | Bits | Approach |
|---|---|---|
| GPTQ | 3–4 bit | Layer-wise quantization using Hessian information; column-wise greedy minimisation |
| AWQ | 4 bit | Weights × activation-scale; protects salient weights |
| **NF4 (QLoRA)** | 4 bit | Optimal for normal-distributed weights |
| bitsandbytes INT8 | 8 bit | LLM.int8() — row-wise quantization with outlier decomposition |

## Quality vs. Bit Width

| Bits | Quality loss (vs. FP16) | Memory saving |
|---|---|---|
| 8-bit | <1% on benchmarks | 2× |
| 4-bit | 1–3% | 4× |
| 3-bit | 3–7% | 5.3× |
| 2-bit | Significant | 8× |

> [!warning] Activation Quantization
> Quantizing activations (W4A4) is harder than weight-only quantization because activations have outliers (large values in specific channels). Techniques like SmoothQuant redistribute the quantization difficulty from activations to weights.

## Significance

Quantization is the primary technique for deploying LLMs on edge devices and consumer hardware. INT4 weight quantization (GPTQ, AWQ) is the standard for local LLM deployment (llama.cpp, Ollama).
