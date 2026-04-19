**Tags:** #concept #rl
**Related:** [[Double Q-Learning]], [[Q-Learning]], [[Action Value Function]], [[Temporal Differences]]

## Definition

Maximization bias is a systematic positive overestimation of action values that arises when the maximum over noisy value estimates is used as an approximation of the maximum true value.

> [!info] Key Intuition
> The maximum of a set of random variables with zero mean is always positive. Using this maximum as a target introduces an upward bias that never cancels, causing the agent to overvalue uncertain actions.

## Mechanism

Consider a state $s$ where all true action values $q(s, a) = 0$. The estimates $Q(s, a)$ are noisy and distributed above and below zero. The maximum of the estimates is always positive:

$$\mathbb{E}\left[\max_a Q(s,a)\right] > \max_a q(s,a) = 0$$

This bias propagates backwards through Bellman updates: overestimated leaf values inflate parent estimates, causing the entire value function to be too optimistic.

Algorithms affected: Q-learning (uses $\max_a Q$), $\varepsilon$-greedy SARSA (policy update uses $\max_a Q$).

> [!example]- Illustrative Example
> In the "maximization bias example" (Sutton & Barto Ch. 6): from state A, going left leads to state B which has many actions all with true expected return $-0.1$ (drawn from $\mathcal{N}(-0.1, 1)$). Going right gives reward 0. Optimal: go right. Q-learning overestimates the value of "go left" because $\max_a Q_B(a)$ is consistently positive due to sampling noise, leading to ~70% left-action selections in early learning.

## Solutions

| Approach | Mechanism |
|---|---|
| [[Double Q-Learning]] | Separate tables for selection vs evaluation |
| Double DQN | Online net selects action; target net evaluates |
| Clipped Double Q | Take minimum of two Q estimates (used in SAC, TD3) |

> [!warning] Common Misconception
> Maximization bias is not the same as overconfidence from limited data. It persists even with infinite data if a single estimator is used for both selecting and evaluating the greedy action.

## Significance

Maximization bias is a fundamental flaw in all greedy value-based methods. Recognising it motivates the entire class of double-estimator algorithms that underpin modern deep RL (Double DQN, TD3, SAC).
