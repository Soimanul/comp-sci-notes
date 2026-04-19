**Tags:** #concept #rl
**Related:** [[Q-Learning]], [[Maximization Bias]], [[SARSA]], [[Temporal Difference Learning]], [[Temporal Differences]]

## Definition

Double Q-learning is an off-policy TD control algorithm that uses two independent action-value estimators, $Q_1$ and $Q_2$, to decouple action selection from action evaluation — eliminating the maximization bias present in standard Q-learning.

> [!info] Key Intuition
> In Q-learning, the same values are used to both choose the best action and evaluate it, inflating estimates. Double Q-learning asks: "one table picks the action, the other table scores it" — the bias cancels out on average.

## Maximization Bias Problem

Standard Q-learning uses $\max_a Q(S_{t+1}, a)$ as the target. When $Q$ estimates carry noise, the maximum of noisy estimates is systematically higher than the true maximum. This **maximization bias** causes Q-learning to overestimate action values and pursue suboptimal actions early in training.

> [!example]- Illustrative Example
> State A has two actions: go left (to state B with many noisy-reward actions) or go right (terminal, reward 0). True optimal: go right (expected return ~0). Q-learning chooses left ~90% of early episodes because the noisy estimates at B have a high maximum by chance. Double Q-learning quickly learns to go right, matching the optimal 5% left-action frequency.

## Update Rule

With probability 0.5, update $Q_1$ using $Q_2$ to evaluate:

$$Q_1(S, A) \leftarrow Q_1(S, A) + \alpha\left(R + \gamma Q_2\!\left(S', \operatorname{argmax}_a Q_1(S', a)\right) - Q_1(S, A)\right)$$

Otherwise (probability 0.5), update $Q_2$ symmetrically using $Q_1$:

$$Q_2(S, A) \leftarrow Q_2(S, A) + \alpha\left(R + \gamma Q_1\!\left(S', \operatorname{argmax}_a Q_2(S', a)\right) - Q_2(S, A)\right)$$

Action selection uses $\varepsilon$-greedy on $Q_1 + Q_2$.

> [!warning] Common Misconception
> Double Q-learning does not eliminate bias entirely — it reduces it. The two estimators are trained on overlapping data (since both see all transitions), so they are not truly independent. In practice the bias is substantially reduced but not zero.

## Significance

The Double Q-learning principle scales directly to deep RL: Double DQN (van Hasselt et al., 2016) applies it by using the online network to select actions and the target network to evaluate them, significantly reducing overestimation in Atari game-playing agents.
