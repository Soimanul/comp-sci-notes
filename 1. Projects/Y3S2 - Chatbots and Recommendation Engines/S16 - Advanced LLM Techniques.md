**Tags:** #hub #llm
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> Deploying LLMs at scale requires a set of optimisation techniques: architectural (MoE, MQA/GQA), inference (KV caching, paged attention, speculative decoding, flash attention, kernel fusion), and training (ZeRO, mixed precision, LoRA/QLoRA, quantization). Alignment alternatives to RLHF include DPO and GRPO/RLVR.

## Overview

Production LLMs are orders of magnitude larger than can be naively served. This session surveys every major technique for making LLM training and inference efficient, and the latest alignment algorithms beyond RLHF.

## Knowledge Map

- [[Mixture of Experts]]
- [[KV Caching]]
- [[Paged Attention]]
- [[RoPE (Rotary Position Embedding)]]
- [[Kernel Fusion]]
- [[Flash Attention]]
- [[Multi-Query and Grouped-Query Attention]]
- [[ZeRO Optimizer]]
- [[Mixed Precision Training]]
- [[LoRA]]
- [[QLoRA]]
- [[LLM Quantization]]
- [[Speculative Decoding]]
- [[PPO for LLM Alignment]]
- [[DPO (Direct Preference Optimization)]]
- [[GRPO and RLVR]]

> [!question]- Exam Questions
> - How does Mixture of Experts reduce per-token compute while increasing model capacity?
> - What is KV caching and why does it speed up autoregressive generation?
> - How does paged attention solve the memory fragmentation problem in KV caching?
> - Explain the LoRA approach: what matrices are updated and why is it parameter-efficient?
> - What is the core idea behind speculative decoding and what is the acceptance criterion?
> - How does DPO remove the need for an explicit reward model compared to PPO-based RLHF?
> - What does GRPO/RLVR replace in the standard RLHF pipeline?
