**Tags:** #concept #rl
**Related:** [[SARSA]], [[Q-Learning]], [[Bellman Equation]], [[Model-Based vs Model-Free RL]]

## Definition

Temporal Difference (TD) learning is a family of model-free RL methods that update value estimates by bootstrapping: using the current estimate of the next state's value as a target, rather than waiting for the full episode return (Monte Carlo).

> [!info] Key Intuition
> Instead of waiting until the end of an episode to see the total return, TD methods update after every step using a one-step look-ahead estimate. The "temporal difference" is the error between the predicted value and the immediately better estimate.

## TD(0) Update

The simplest TD update for state-value estimation:

$$V(S_t) \leftarrow V(S_t) + \alpha\left[\underbrace{R_{t+1} + \gamma V(S_{t+1})}_{\text{TD target}} - V(S_t)\right]$$

The **TD error** $\delta_t = R_{t+1} + \gamma V(S_{t+1}) - V(S_t)$ is the signed difference between the current estimate and the bootstrapped target.

## TD vs Monte Carlo vs DP

| | DP | Monte Carlo | TD |
|---|---|---|---|
| Needs model? | Yes (full backup) | No (sample) | No (sample) |
| Updates when? | After sweep | End of episode | After each step |
| Bootstrap? | Yes | No | Yes |
| Bias | None | None | Yes (bootstrap bias) |
| Variance | Low | High | Low |

TD is the intersection of DP bootstrapping and MC sampling — it is the "best of both worlds" for most practical problems.

## Convergence

TD(0) converges to $v_\pi$ under the following conditions:
- Step-size satisfies $\sum_t \alpha_t = \infty$ and $\sum_t \alpha_t^2 < \infty$
- All states visited infinitely often under policy $\pi$

> [!warning] Common Misconception
> TD is not guaranteed to converge to $v_\pi$ with function approximation (e.g. neural networks) and off-policy data — this is the "deadly triad" problem. Tabular TD always converges; deep RL requires careful stabilisation (target networks, experience replay in DQN).

## Significance

TD learning is the core mechanism of SARSA, Q-learning, and all temporal credit assignment in deep RL. The TD error signal is biologically plausible and mirrors dopamine prediction error in neuroscience.
