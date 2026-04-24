**Tags:** #concept #dl #llm
**Related:** [[ZeRO Optimizer]], [[QLoRA]], [[LLM Quantization]]

## Definition

**Mixed precision training** uses lower-precision floating point formats (FP16 or BF16) for the forward/backward pass to reduce memory and increase throughput, while maintaining FP32 **master weights** and optimizer states to preserve numerical precision and training stability.

> [!info] Key Intuition
> FP16 uses 2 bytes per value vs. FP32's 4 bytes — halves memory and doubles throughput on Tensor Cores. But FP16 has limited dynamic range, causing gradient overflow/underflow. Mixed precision keeps only the critical precision-sensitive values (optimizer states, master weights) in FP32.

## Formats

| Format | Bits | Mantissa | Range | Use |
|---|---|---|---|---|
| FP32 | 32 | 23 bits | Wide | Master weights, optimizer states |
| FP16 | 16 | 10 bits | Narrow | Forward/backward activations, gradients |
| BF16 | 16 | 7 bits | Wide (same as FP32) | Preferred for LLM training (no overflow) |

**BF16 is preferred** over FP16 for LLM training because it has the same exponent range as FP32 (preventing overflow), at the cost of less mantissa precision (which is usually acceptable).

## Mixed Precision Training Steps

1. **Store** master weights in FP32
2. **Cast** to FP16/BF16 before forward pass
3. **Forward pass** in FP16/BF16 → compute activations and loss
4. **Loss scaling** (FP16 only): multiply loss by a large scalar to prevent gradient underflow
5. **Backward pass** in FP16/BF16 → compute gradients
6. **Unscale gradients** → convert to FP32
7. **Update** FP32 master weights with FP32 optimizer states

## Memory Savings

For a model with $\Psi$ parameters:
| Component | FP32 | Mixed |
|---|---|---|
| Model weights | $4\Psi$ | $2\Psi$ (FP16/BF16) + $4\Psi$ (master) |
| Gradients | $4\Psi$ | $2\Psi$ |
| Adam states | $8\Psi$ | $8\Psi$ (FP32) |
| **Total** | $16\Psi$ | $\approx 16\Psi$ (same) |

The main saving is on activation memory during the forward pass, and on Tensor Core throughput.

> [!warning] Gradient Overflow (FP16)
> FP16's small range causes gradient underflow at the small end. **Loss scaling** multiplies the loss (and thus all gradients) by a large constant (e.g. 2^15) before backprop, then divides after. PyTorch's `GradScaler` handles this automatically.

## Significance

Mixed precision training is universally used in LLM training, typically halving memory for activations and doubling throughput on modern GPUs with Tensor Cores (A100, H100). PyTorch's `torch.autocast` enables it with minimal code changes.
