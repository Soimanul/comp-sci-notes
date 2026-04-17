**Tags:** #concept #rl
**Related:** [[Temporal Difference Learning]], [[Q-Learning]], [[Expected SARSA]], [[RL Policy]]

## Definition

SARSA (State-Action-Reward-State-Action) is an **on-policy** TD control algorithm that learns the action-value function $Q(s,a) \approx q_\pi(s,a)$ for the policy being followed, including its exploratory actions.

> [!info] Key Intuition
> SARSA learns the value of the policy it actually executes — including its exploration steps. This makes it conservative: if the current ε-greedy policy sometimes walks off a cliff, SARSA learns that the cliff-edge states are dangerous.

## Update Rule

After each step $(S_t, A_t, R_{t+1}, S_{t+1}, A_{t+1})$:

$$Q(S_t, A_t) \leftarrow Q(S_t, A_t) + \alpha\left[R_{t+1} + \gamma\, Q(S_{t+1}, A_{t+1}) - Q(S_t, A_t)\right]$$

The name SARSA comes from the five elements of the transition tuple used in the update.

## On-Policy Nature

$A_{t+1}$ is sampled from the current policy $\pi$ (e.g. ε-greedy). The target $R_{t+1} + \gamma Q(S_{t+1}, A_{t+1})$ reflects what actually happens under $\pi$, including exploratory moves.

**Consequence**: In the RL maze testbed, SARSA learns to avoid water tiles because it accounts for the cost of accidentally stepping into water under the exploratory policy.

## Convergence

SARSA converges to $q_*$ if:
1. The policy converges to greedy in the limit (e.g. GLIE — Greedy in the Limit with Infinite Exploration)
2. Step sizes satisfy Robbins-Monro conditions

> [!example]- Worked Example
> Windy gridworld: agent navigates a grid with per-column wind pushing it upward. SARSA with ε=0.1 learns to approach the goal diagonally against the wind, converging faster than random exploration because it evaluates paths under its actual navigating policy.

> [!warning] Common Misconception
> SARSA does not learn $q_*$ — it learns $q_\pi$ for the current (ε-greedy) policy. To obtain $q_*$, you need to reduce ε → 0 over time, or use Q-learning.

## Significance

SARSA is the canonical on-policy TD method. Its conservative behaviour makes it preferable over Q-learning in problems where exploratory actions carry real costs (e.g. physical robots, safety-critical systems).
