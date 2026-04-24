**Tags:** #concept #llm
**Related:** [[Mixed Precision Training]], [[Transformer Architecture]]

## Definition

**ZeRO (Zero Redundancy Optimizer)** is a distributed training memory optimisation technique that eliminates model state redundancy across data-parallel workers by partitioning optimizer states, gradients, and/or model parameters across GPUs rather than replicating them.

> [!info] Key Intuition
> In standard data-parallel training, every GPU holds a full copy of the model, gradients, and optimizer states — pure redundancy. ZeRO says: if you have 8 GPUs, let each GPU hold only 1/8 of each state. Communication handles the rest. You get the same throughput but 8× less memory per GPU.

## Three Optimisation Stages

| Stage | What is partitioned | Memory reduction |
|---|---|---|
| **ZeRO-1** | Optimizer states | ~4× |
| **ZeRO-2** | + Gradients | ~8× |
| **ZeRO-3** | + Model parameters | linear in $N_{\text{GPUs}}$ |

For a model with $\Psi$ parameters, Adam optimizer states use $12\Psi$ bytes (fp32 params + gradients + 2 moments). With $N$ GPUs, ZeRO-3 reduces per-GPU usage to $12\Psi / N$.

## ZeRO-Infinity

Extends ZeRO-3 to offload to CPU memory or NVMe storage for even larger models, at the cost of communication bandwidth.

## Communication Overhead

ZeRO-1/2: same communication volume as standard data-parallel (allreduce gradients).
ZeRO-3: increases communication volume by ~50% due to gather/scatter of parameters, but the memory savings typically outweigh this cost.

> [!example]- GPT-3 (175B) Training
> On 400 V100 GPUs with ZeRO-3, each GPU holds only 175B × 12 / 400 ≈ 5.25B bytes of optimizer state ≈ 5.25 GB, instead of 2.1 TB. This made training GPT-3 scale tractable.

## Implementation

ZeRO is implemented in Microsoft **DeepSpeed** and has been integrated into Hugging Face Accelerate and PyTorch FSDP (Fully Sharded Data Parallel), which is a native PyTorch equivalent.

## Significance

ZeRO enabled training 10B–trillion parameter models on clusters of commodity GPUs. Without it, large LLM training would require either model parallelism (complex) or extremely expensive high-memory GPUs.
