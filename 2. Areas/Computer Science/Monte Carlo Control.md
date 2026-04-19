**Tags:** #concept #rl
**Related:** [[Monte Carlo Methods]], [[Monte Carlo Prediction]], [[Generalized Policy Iteration]], [[Action Value Function]], [[Exploring Starts]]

## Definition

Monte Carlo Control is the application of Generalised Policy Iteration (GPI) to find the optimal policy $\pi_*$ using only sampled episodes, without a model. It alternates between Monte Carlo policy evaluation (estimating $q_\pi$) and greedy policy improvement.

> [!info] Key Intuition
> Because no model is available, the agent must estimate action-value functions $q_\pi(s,a)$ rather than state-value functions — only $q$ allows choosing the best action without knowing transition dynamics.

## Why Action Values, Not State Values

With a model, state values alone are sufficient: one step of lookahead identifies the best action. Without a model, the agent cannot determine which action leads to the best next state. Estimating $q_\pi(s,a)$ directly for each state-action pair makes the greedy policy constructible without any environment model:

$$\pi(s) = \arg\max_a q(s, a)$$

## GPI Structure for MC Control

The control cycle follows the same pattern as DP:

$$\pi_0 \xrightarrow{E} q_{\pi_0} \xrightarrow{I} \pi_1 \xrightarrow{E} q_{\pi_1} \xrightarrow{I} \cdots \xrightarrow{I} \pi_* \xrightarrow{E} q_*$$

where $E$ is MC policy evaluation and $I$ is greedy improvement: $\pi(s) \leftarrow \arg\max_a Q(s,a)$.

## Convergence Assumptions

Two assumptions are required for guaranteed convergence:

1. **Infinite episodes for evaluation**: policy evaluation is performed with enough episodes to get an accurate $q$ estimate. In practice, this is relaxed by alternating evaluation and improvement on an episode-by-episode basis.
2. **Exploring Starts**: every state-action pair must have a nonzero probability of being selected as the episode start, ensuring all pairs are visited infinitely often.

Assumption 2 is relaxed by using $\varepsilon$-soft policies (On-Policy MC) or Importance Sampling (Off-Policy MC).

## Incremental Update

The average of returns can be computed incrementally, avoiding storage of all past returns:

$$Q(S_t, A_t) \leftarrow Q(S_t, A_t) + \frac{1}{N(S_t, A_t)}\left[G - Q(S_t, A_t)\right]$$

where $N(S_t, A_t)$ is the count of visits to the pair.

> [!example]- Worked Example — Blackjack with MC ES
> Initialize $Q(s,a)$ arbitrarily. Each episode starts at a randomly chosen $(S_0, A_0)$ pair (Exploring Starts). After computing $G$ backward through the episode, update $Q(S_t, A_t)$ for first visits and set $\pi(S_t) \leftarrow \arg\max_a Q(S_t, a)$. After sufficient episodes, the optimal policy (stick at 20 or 21, hit otherwise) and its value function emerge.

> [!warning] Common Misconception
> MC control updates the policy after each complete episode, not after each step. This episode-by-episode granularity makes MC control slower to respond than TD-based control methods such as SARSA or Q-learning.

## Significance

MC control establishes that optimal policies can be found from pure experience, with no model. The action-value formulation is essential here and carries forward to all subsequent model-free control methods.
