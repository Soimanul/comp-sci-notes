**Tags:** #concept #rl
**Related:** [[SARSA]], [[Q-Learning]], [[Temporal Difference Learning]]

## Definition

Expected SARSA is a TD control algorithm that uses the **expected value** over the current policy's action distribution as the TD target, rather than the sampled next action (SARSA) or the max (Q-learning):

$$Q(S_t,A_t) \leftarrow Q(S_t,A_t) + \alpha\left[R_{t+1} + \gamma \sum_{a'} \pi(a'|S_{t+1})\, Q(S_{t+1},a') - Q(S_t,A_t)\right]$$

> [!info] Key Intuition
> Expected SARSA removes the variance of SARSA's random action sample $A_{t+1}$ by averaging over all possible next actions. With the same data, it is typically more stable than SARSA.

## Relationship to SARSA and Q-learning

- **SARSA**: samples $A_{t+1} \sim \pi(\cdot|S_{t+1})$, uses $Q(S_{t+1}, A_{t+1})$ — high variance
- **Expected SARSA**: averages $\sum_{a'} \pi(a'|S_{t+1}) Q(S_{t+1},a')$ — lower variance, slightly more compute
- **Q-learning**: uses $\max_{a'} Q(S_{t+1},a')$ — if $\pi$ is greedy, Expected SARSA = Q-learning

Expected SARSA generalises both: if $\pi$ is ε-greedy, the target interpolates between the mean and the max.

## Empirical Performance

In the RL maze testbed, Expected SARSA converges faster and more stably than both SARSA and Q-learning, especially early in training when $Q$ estimates are noisy.

> [!warning] Common Misconception
> Expected SARSA can be both on-policy (if the same $\pi$ is used for behaviour and the expectation) or off-policy (if a different target policy is used in the expectation). Using the greedy policy in the expectation makes it equivalent to Q-learning — it is the most general of the three algorithms.

## Significance

Expected SARSA demonstrates that reducing variance (by taking expectations) consistently outperforms sampling. This principle extends to actor-critic methods where baseline subtraction and advantage estimation serve the same role.
