**Tags:** #concept #llm
**Related:** [[QLoRA]], [[Fine-tuning in NLP]], [[ZeRO Optimizer]]

## Definition

**LoRA (Low-Rank Adaptation)** is a parameter-efficient fine-tuning method that freezes the pre-trained model weights and injects trainable **low-rank decomposition matrices** into specific layers, achieving fine-tuning quality close to full fine-tuning with only 0.01–1% of the trainable parameters.

> [!info] Key Intuition
> A weight matrix $W \in \mathbb{R}^{d \times k}$ contains $d \times k$ parameters. LoRA says the fine-tuning update $\Delta W$ has low intrinsic rank — it can be approximated by two small matrices $A \in \mathbb{R}^{d \times r}$ and $B \in \mathbb{R}^{r \times k}$ where $r \ll \min(d,k)$. Train $A, B$ instead of $W$.

## Method

**During training:**
- Freeze original weight $W_0$
- Add: $W = W_0 + \Delta W = W_0 + BA$
- Only $A$ and $B$ are updated; $W_0$ never changes
- Initialise: $B = 0$, $A \sim \mathcal{N}(0, \sigma^2)$ → initially $\Delta W = 0$

**Forward pass:**
$$h = W_0 x + \Delta W x = W_0 x + B A x$$

Scale: $\Delta W = \frac{\alpha}{r} B A$ where $\alpha$ is a hyperparameter controlling the update magnitude.

## Parameter Count

For attention weight $W_q \in \mathbb{R}^{d \times d}$ with rank $r$:
- Original: $d^2$ parameters
- LoRA: $2dr$ parameters
- For $d = 4096, r = 16$: $16.7M$ → $131K$ (126× reduction)

## LoRA is Applied To:

Typically the query and value projection matrices in self-attention:
$$W_q, W_v \text{ (most impactful)}; W_k, W_o, \text{FFN matrices (optional)}$$

## Hyperparameters

| Parameter | Typical values | Effect |
|---|---|---|
| `r` (rank) | 4, 8, 16, 32 | Higher = more expressive, more params |
| `α` (scaling) | = r or 2r | Controls update magnitude |
| `target_modules` | q_proj, v_proj | Which weight matrices to adapt |

## Merging at Inference

After training, LoRA weights can be **merged** into the base model: $W = W_0 + BA$ — no inference overhead. Or kept separate for multi-task switching.

## Significance

LoRA made fine-tuning 65B+ parameter models feasible on a single GPU and enabled the "fine-tune on a personal laptop" workflow. It is implemented in Hugging Face PEFT and is the standard approach for LLM customisation in both research and production.
