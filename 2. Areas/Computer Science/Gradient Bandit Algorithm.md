**Tags:** #concept #rl
**Related:** [[Multi-Armed Bandits]], [[k-Armed Bandit Problem]], [[Exploration-Exploitation Tradeoff]]

## Definition

A bandit algorithm that learns a numerical **preference** $H_t(a)$ for each action rather than estimating action values directly. Actions are selected according to a softmax distribution over preferences, and preferences are updated via stochastic gradient ascent on expected reward.

> [!info] Key Intuition
> Instead of "arm 3 gives reward ≈ 1.5," the gradient bandit thinks "arm 3 is preferred with score 2.1." Only relative preferences matter — adding a constant to all $H_t(a)$ leaves the policy unchanged.

## Softmax Policy

$$\pi_t(a) = \frac{e^{H_t(a)}}{\sum_{b=1}^k e^{H_t(b)}}$$

## Stochastic Gradient Ascent Update

After selecting $A_t$ and receiving $R_t$:

$$H_{t+1}(A_t) = H_t(A_t) + \alpha(R_t - \bar{R}_t)(1 - \pi_t(A_t))$$
$$H_{t+1}(a) = H_t(a) - \alpha(R_t - \bar{R}_t)\pi_t(a) \quad \text{for } a \neq A_t$$

where $\bar{R}_t$ is the **reward baseline** (running average of all past rewards).

## Role of the Baseline

- If $R_t > \bar{R}_t$: the selected action's preference increases; all others decrease
- If $R_t < \bar{R}_t$: the selected action is penalised; others are relatively boosted
- Without the baseline ($\bar{R}_t = 0$), performance degrades significantly when rewards are shifted away from zero (the algorithm becomes scale-sensitive)

> [!example]- Worked Example
> 10-armed bandit with $q_*(a) \sim \mathcal{N}(+4, 1)$. Without baseline: all rewards look "good" ($R_t > 0$), so the selected action is always reinforced regardless of whether it was actually above average. With baseline: the algorithm correctly distinguishes above-average from below-average.

> [!warning] Common Misconception
> Gradient bandits do not estimate action values at all. They cannot be used to compute a greedy policy in the usual sense — the policy is always stochastic (softmax). The preferences have no absolute meaning, only relative.

## Significance

The gradient bandit is the bandit analogue of policy gradient methods in full RL (REINFORCE, PPO). The baseline $\bar{R}_t$ foreshadows the advantage function in actor-critic algorithms.
