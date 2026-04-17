**Tags:** #concept #rl
**Related:** [[Multi-Armed Bandits]], [[Action-Value Estimation]], [[Exploration-Exploitation Tradeoff]]

## Definition

A repeated decision problem with $k$ actions (arms), each with a stationary but unknown reward distribution. At each time step, the agent selects one action and receives a stochastic reward sampled from that action's distribution. The goal is to maximise cumulative reward.

> [!info] Key Intuition
> Think of $k$ slot machines: each has a different expected payout, and you can only pull one lever per round. You must discover the best machine while losing as little as possible on suboptimal machines.

## Formal Setup

- $k$ actions $a \in \{1, \ldots, k\}$
- True action value: $q_*(a) = \mathbb{E}[R_t \mid A_t = a] = \sum_r p(r|a)\,r$
- Agent estimates: $Q_t(a) \approx q_*(a)$ updated from observed rewards
- Greedy action: $A_t^* = \arg\max_a Q_t(a)$

**Types:**
- **Stochastic MAB**: rewards drawn from fixed unknown distributions
- **Adversarial MAB**: rewards chosen by an adversary (minimax regret)
- **Bernoulli bandit**: rewards are 0 or 1 with unknown probability $\theta_k$

## Regret

The expected regret after $T$ steps:
$$\text{Regret}(T) = T \cdot q_*(a^*) - \sum_{t=1}^T \mathbb{E}[R_t]$$

where $a^*$ is the optimal arm. Good algorithms achieve sublinear regret — they eventually converge to near-optimal behaviour.

> [!example]- Worked Example
> 10-armed testbed: $k=10$, $q_*(a) \sim \mathcal{N}(0,1)$, rewards $\sim \mathcal{N}(q_*(a),1)$. After 1000 steps, ε=0.1 greedy achieves ~80% optimal action selection; UCB achieves ~90%.

> [!warning] Common Misconception
> The k-armed bandit is **non-associative** — there is only one state. The agent does not need to learn a policy mapping states to actions, only which action is best in this single, fixed situation.

## Significance

The bandit problem is the canonical testbed for exploration strategies. Every idea tested here (ε-greedy, UCB, Thompson Sampling) extends to the full RL setting.
