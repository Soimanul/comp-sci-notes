**Tags:** #concept #llm
**Related:** [[RLHF]], [[PPO for LLM Alignment]], [[GRPO and RLVR]]

## Definition

**DPO (Direct Preference Optimization)** is a simpler alternative to RLHF that directly fine-tunes the LLM on human preference pairs without an explicit reward model or RL training loop, by deriving a closed-form relationship between the optimal policy and the reward function.

> [!info] Key Intuition
> RLHF requires: (1) train a reward model, (2) use PPO with 4 models. DPO shows that you can skip both steps — the optimal RLHF policy can be expressed directly as a function of the LLM's log probabilities on preferred vs. rejected responses. Just optimise that directly.

## Derivation

The optimal RLHF policy is:
$$\pi^*(y|x) = \frac{1}{Z(x)} \pi_{\text{ref}}(y|x) \exp\left(\frac{1}{\beta} r(x,y)\right)$$

Solving for the reward in terms of the optimal policy:
$$r(x,y) = \beta \log \frac{\pi^*(y|x)}{\pi_{\text{ref}}(y|x)} + \beta \log Z(x)$$

Substituting into the Bradley-Terry preference model and noting $Z(x)$ cancels:

## DPO Objective

$$L_{\text{DPO}}(\theta) = -\mathbb{E}_{(x, y_w, y_l)} \left[\log \sigma\left(\beta \log \frac{\pi_\theta(y_w|x)}{\pi_{\text{ref}}(y_w|x)} - \beta \log \frac{\pi_\theta(y_l|x)}{\pi_{\text{ref}}(y_l|x)}\right)\right]$$

Where $y_w$ = preferred response, $y_l$ = rejected response.

**Interpretation:** Increase the relative log-probability of $y_w$ over $y_l$, compared to the reference model.

## DPO vs. RLHF-PPO

| Property | RLHF-PPO | DPO |
|---|---|---|
| Reward model | Explicit (trained separately) | Implicit (absorbed into policy objective) |
| RL algorithm | PPO | None (supervised classification-style) |
| Number of models | 4 (policy, ref, reward, value) | 2 (policy, ref) |
| Stability | Requires tuning | More stable |
| Flexibility | Any reward | Preference data only |
| Performance | Slightly better on complex tasks | Comparable on most tasks |

> [!warning] DPO Limitations
> DPO is offline — it trains on a fixed preference dataset. PPO can explore by generating new responses. For complex reasoning tasks (math, code) where exploration matters, PPO or [[GRPO and RLVR]] can outperform DPO.

## Significance

DPO (Rafailov et al., 2023) simplified LLM alignment dramatically: no reward model training, no PPO, 2 models instead of 4. It became the default alignment method for open-source models (LLaMA fine-tunes, Zephyr, Tulu) and is available in Hugging Face TRL.
