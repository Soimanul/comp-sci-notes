**Tags:** #concept #rl
**Related:** [[k-Armed Bandit Problem]], [[Exploration-Exploitation Tradeoff]], [[Action-Value Estimation]]

## Definition

A simple action selection policy that exploits the current best estimate most of the time but explores uniformly at random with probability ε:

$$A_t = \begin{cases} \arg\max_a Q_t(a) & \text{with probability } 1-\varepsilon \\ \text{random } a \in \mathcal{A} & \text{with probability } \varepsilon \end{cases}$$

> [!info] Key Intuition
> ε-greedy guarantees that every action is tried infinitely often as $t \to \infty$, ensuring all $Q_t(a) \to q_*(a)$. This is the minimal viable exploration strategy.

## Properties

- **ε = 0** (pure greedy): no exploration, converges to local optimum
- **ε = 1** (pure random): no exploitation, never uses what it has learned
- **ε ∈ (0,1)**: balances both; typically ε = 0.01 or 0.1 in practice

The ε fraction of steps is wasted on suboptimal actions in the limit, so **greedy with optimistic initialization** or **UCB** are preferred when the environment is stationary.

## Epsilon Decay

For stationary problems, decaying ε (e.g. $\varepsilon_t = 1/t$) can achieve near-optimal convergence. For non-stationary problems, ε should remain constant to allow re-exploration after distribution shifts.

> [!example]- Worked Example
> 10-armed bandit: ε=0.1 greedy. At $t=100$, $Q_t(3) = 1.5$ is the current best estimate. With 90% probability, the agent pulls arm 3. With 10% probability, it picks uniformly from arms 1-10 (may pull arm 3 again, or try arm 7).

> [!warning] Common Misconception
> ε-greedy does **not** direct exploration toward uncertain arms. It wastes exploration budget on arms already known to be bad. UCB is strictly smarter: it explores arms proportional to their uncertainty.

## Significance

ε-greedy is the baseline exploration strategy used in Q-learning, DQN, and most tabular RL algorithms due to its simplicity. Its main limitation is uniform exploration regardless of uncertainty.
