**Tags:** #concept #llm #rl
**Related:** [[RLHF]], [[DPO (Direct Preference Optimization)]], [[GRPO and RLVR]]

## Definition

**PPO for LLM Alignment (Proximal Policy Optimization)** is the reinforcement learning algorithm used in the RLHF pipeline to fine-tune a language model to maximise a reward model's scores while remaining close to the original SFT model, using clipped surrogate objectives to ensure stable updates.

> [!info] Key Intuition
> After training a reward model on human preferences, we want to update the LLM to get higher rewards. Plain policy gradient is unstable (large updates can catastrophically change the model). PPO clips the update size to ensure the new policy doesn't deviate too far from the old one — stable online RL for LLMs.

## PPO Objective for LLMs

$$L^{CLIP}(\theta) = \mathbb{E}_t \left[ \min\left( r_t(\theta) \hat{A}_t,\ \text{clip}(r_t(\theta), 1-\epsilon, 1+\epsilon) \hat{A}_t \right) \right]$$

Where:
- $r_t(\theta) = \frac{\pi_\theta(a_t|s_t)}{\pi_{\theta_{\text{old}}}(a_t|s_t)}$ = probability ratio (new vs old policy)
- $\hat{A}_t$ = advantage estimate (reward minus value baseline)
- $\epsilon$ = clip hyperparameter (typically 0.2)

## Full RLHF-PPO Objective

$$L = L^{CLIP} - \beta \cdot \text{KL}(\pi_\theta \| \pi_{\text{ref}})$$

The KL penalty:
- $\pi_\theta$ = current LLM being trained
- $\pi_{\text{ref}}$ = frozen SFT reference model
- $\beta$ = KL coefficient (prevents reward hacking)

## Four Models in RLHF-PPO

| Model | Role | Updated? |
|---|---|---|
| Policy ($\pi_\theta$) | The LLM being aligned | Yes (PPO updates) |
| Reference ($\pi_{\text{ref}}$) | Frozen SFT baseline for KL | No |
| Reward model ($r_\phi$) | Scores generated responses | No |
| Value model | Estimates expected reward (baseline) | Yes (critic) |

## Advantages of PPO for RLHF

- Stable updates via clipping
- Can optimise any differentiable reward signal
- KL penalty prevents degenerate outputs

## Limitations

- Requires maintaining 4 models simultaneously → high GPU memory
- Sensitive to hyperparameters (KL weight $\beta$, clip $\epsilon$)
- Complex to implement → motivated [[DPO (Direct Preference Optimization)]]

## Significance

PPO is the algorithm behind InstructGPT/ChatGPT's alignment. Despite its complexity, it remains the most flexible RLHF approach for complex reward functions (e.g. combining helpfulness + safety).
