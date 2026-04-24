**Tags:** #concept #llm
**Related:** [[DPO (Direct Preference Optimization)]], [[PPO for LLM Alignment]], [[RLHF]]

## Definition

**GRPO (Group Relative Policy Optimization)** is a reinforcement learning alignment algorithm that removes the value/critic model from PPO by estimating advantages using the group relative scores of multiple sampled responses. **RLVR (Reinforcement Learning with Verifiable Rewards)** is the paradigm of using programmatically verifiable reward signals (correctness, test passing, format compliance) instead of human preference rewards to train reasoning models.

> [!info] Key Intuition
> GRPO: instead of a value network estimating expected reward, sample $G$ responses for the same prompt, compute their actual rewards, and normalise by the group's mean and variance. This provides a relative advantage estimate without needing a separate critic.
> RLVR: if the reward is "does the code pass the test?" or "is the math answer correct?", we don't need human labellers — just run a checker.

## GRPO Algorithm

For a prompt $x$, sample $G$ responses $\{y_1, \ldots, y_G\}$ from the current policy.

**Advantage for response $i$:**
$$\hat{A}_i = \frac{r_i - \text{mean}(\{r_j\}_{j=1}^G)}{\text{std}(\{r_j\}_{j=1}^G)}$$

**Objective (similar to PPO clipping):**
$$L_{\text{GRPO}} = -\mathbb{E}\left[\sum_{i=1}^G \min\left(r_t(\theta) \hat{A}_i, \text{clip}(r_t(\theta), 1-\epsilon, 1+\epsilon) \hat{A}_i\right) - \beta \cdot \text{KL}(\pi_\theta \| \pi_{\text{ref}})\right]$$

## Advantages Over PPO

| Property | PPO | GRPO |
|---|---|---|
| Value model | Required | Not needed |
| Memory (models) | 4 | 3 (policy, ref, reward) |
| Advantage estimation | Critic prediction | Group relative normalisation |
| Implementation complexity | High | Lower |

## RLVR: Verifiable Rewards

RLVR replaces the human-trained reward model with a **verifier** that programmatically scores responses:

| Domain | Verifiable reward |
|---|---|
| Mathematics | Exact answer match (after parsing) |
| Code | Unit test pass rate |
| Format | JSON validity, length constraint |
| Logic puzzles | Correct solution verification |

**Key advantage:** Scalable. Human labellers become a bottleneck; verifiers can score millions of responses instantly.

## DeepSeek-R1

GRPO + RLVR achieved a breakthrough in mathematical reasoning with DeepSeek-R1 (2025): training on math problems with exact-answer rewards produced chain-of-thought reasoning behaviour that emerged without any explicit reasoning supervision. This influenced the field's interest in RLVR as an alternative to RLHF for reasoning tasks.

## Significance

GRPO+RLVR simplified the RL alignment pipeline and demonstrated that verifiable rewards can produce strong reasoning capabilities, motivating a shift from preference learning to outcome-based RL for domains with checkable answers.
