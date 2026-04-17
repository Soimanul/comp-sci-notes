**Tags:** #concept #rl
**Related:** [[Temporal Difference Learning]], [[SARSA]], [[Expected SARSA]], [[Bellman Optimality Equation]]

## Definition

Q-learning is an **off-policy** TD control algorithm that directly approximates the optimal action-value function $q_*$, independently of the policy being followed.

> [!info] Key Intuition
> Q-learning always imagines taking the best possible action from the next state, regardless of what the actual policy would do. This means it converges to the optimal policy even while exploring sub-optimally.

## Update Rule

$$Q(S_t, A_t) \leftarrow Q(S_t, A_t) + \alpha\left[R_{t+1} + \gamma \max_{a'} Q(S_{t+1}, a') - Q(S_t, A_t)\right]$$

The target $R_{t+1} + \gamma \max_{a'} Q(S_{t+1}, a')$ directly approximates $q_*(S_t, A_t)$ via the Bellman optimality equation.

## Off-Policy Nature

The **behaviour policy** (e.g. ε-greedy) generates experience; the **target policy** is always greedy ($\max_{a'}$). This decoupling allows:
- Learning from demonstrations or replay buffers
- Learning the optimal policy while still exploring
- The basis for DQN (experience replay + target networks)

**Consequence**: Q-learning is optimistic — it assumes future behaviour is optimal. In the maze testbed, Q-learning may walk near water tiles because it imagines never falling in; SARSA avoids them because it accounts for ε-greedy stumbles.

## Convergence

Q-learning converges to $q_*$ if:
1. All $(s,a)$ pairs are visited infinitely often
2. Step sizes satisfy $\sum \alpha_t = \infty$, $\sum \alpha_t^2 < \infty$
3. Rewards are bounded

> [!example]- Worked Example
> Cliff walking: Q-learning finds the optimal shortest path along the cliff edge (shorter path, but risky under ε-greedy). SARSA finds the safe longer path away from the cliff. Both eventually find $q_*$ as ε→0, but SARSA performs better online.

> [!warning] Common Misconception
> Q-learning is off-policy because the **target** uses max, not because the behaviour policy is different from the target policy. Even if you run Q-learning with a greedy behaviour policy, it is still off-policy in the theoretical sense.

## Significance

Q-learning is the foundation of deep RL: DQN (Deep Q-Network, DeepMind 2015) scales Q-learning to high-dimensional state spaces using a neural network to approximate $Q(s,a;\theta)$.
