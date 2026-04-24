**Tags:** #concept #llm
**Related:** [[RLHF vs Cross-Entropy Training]], [[PPO for LLM Alignment]], [[DPO (Direct Preference Optimization)]], [[BERT]]

## Definition

**RLHF (Reinforcement Learning from Human Feedback)** is a three-stage alignment technique that fine-tunes a pre-trained LLM to produce outputs that align with human preferences, using a reward model trained on human comparison data and PPO to optimise the LLM against that reward.

> [!info] Key Intuition
> A language model pre-trained on internet text learns to imitate internet text — not to be helpful, harmless, or honest. RLHF uses human judgements of "which response is better" to define a reward, then uses RL to steer the model towards higher-reward outputs.

## Three Stages

### Stage 1: Supervised Fine-tuning (SFT)
- Collect high-quality (prompt, response) demonstration pairs from human annotators
- Fine-tune the pre-trained LLM on these demonstrations
- Output: SFT model

### Stage 2: Reward Model Training
- Collect preference data: for each prompt, show the model two or more responses, have annotators rank them
- Train a **reward model** $r_\phi(x, y)$ to predict human preference:
$$L_{RM} = -\log \sigma(r_\phi(x, y_w) - r_\phi(x, y_l))$$
where $y_w$ = preferred response, $y_l$ = less preferred response

### Stage 3: PPO Fine-tuning
Optimise the SFT model $\pi_\theta$ to maximise reward while staying close to the SFT policy:
$$\max_{\pi_\theta} \mathbb{E}[r_\phi(x, y)] - \beta \, \text{KL}(\pi_\theta \| \pi_{\text{ref}})$$

The KL penalty $\beta$ prevents reward hacking (producing gibberish that fools the reward model).

## Data Scale (InstructGPT, OpenAI)

| Stage | Data size |
|---|---|
| SFT demonstrations | ~13,000 prompts |
| Preference comparisons | ~33,000 prompts |
| PPO training | ~31,000 prompts |

> [!warning] Reward Hacking
> The RL model can learn to exploit the reward model's weaknesses, producing high-reward but low-quality outputs. The KL penalty and periodic reward model refreshes mitigate this. DPO avoids this problem by removing the explicit reward model.

## Significance

RLHF is the key technique behind ChatGPT, Claude, and other instruction-following LLMs. It is what transforms a next-token predictor into a helpful assistant.
