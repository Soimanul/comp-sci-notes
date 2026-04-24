**Tags:** #concept #llm
**Related:** [[LoRA]], [[LLM Quantization]], [[Mixed Precision Training]]

## Definition

**QLoRA (Quantized Low-Rank Adaptation)** combines 4-bit quantization of the frozen base model with LoRA fine-tuning, enabling fine-tuning of 65B+ parameter LLMs on a single consumer GPU by dramatically reducing the memory footprint of the base model without sacrificing fine-tuning quality.

> [!info] Key Intuition
> LoRA freezes the base model (saving most of the gradient computation) but still requires loading the full FP16 base model into GPU memory. QLoRA quantizes the frozen base model to 4-bit, reducing its memory 4–8×. The small LoRA adapters remain in BF16 for precise gradient computation.

## Three Key Innovations

### 1. NF4 (Normal Float 4-bit)
A new 4-bit data type optimal for normally distributed model weights. Unlike INT4, NF4 has more precision near zero (where most weights cluster) and less precision for large values.

### 2. Double Quantization
Quantize the quantization constants themselves — reduces the memory overhead of storing per-block quantization scales from ~0.5 bits/param to ~0.37 bits/param.

### 3. Paged Optimizers
Uses NVIDIA's unified memory to page optimizer states between CPU and GPU memory during memory spikes (e.g. long sequences), preventing out-of-memory errors without affecting average throughput.

## Memory Comparison (65B model)

| Approach | GPU memory |
|---|---|
| Full BF16 | 130 GB (requires 8+ A100 80GB) |
| LoRA (BF16 base) | 130 GB (base) + small adapters |
| QLoRA (NF4 base) | ~40 GB (fits on single A100 80GB or 2× RTX 3090) |

## Quality

QLoRA fine-tuning achieves performance within ~1% of full 16-bit fine-tuning on standard benchmarks (MMLU, HELM), despite the extreme compression.

## Workflow

```
65B Base Model (NF4, frozen)
        + 
LoRA adapters A, B (BF16, trainable)
        ↓
Forward pass: dequantize weights on-the-fly → compute in BF16
        ↓
Backward pass: gradients flow through LoRA adapters only
        ↓
Update only A, B
```

## Significance

QLoRA (Dettmers et al., 2023) democratised LLM fine-tuning: what required a 8-GPU cluster can now be done on a single consumer GPU. It enabled the open-source LLM fine-tuning ecosystem (Alpaca, Vicuna, WizardLM, etc.).
