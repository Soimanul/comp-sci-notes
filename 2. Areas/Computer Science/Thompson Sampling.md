**Tags:** #concept #rl
**Related:** [[k-Armed Bandit Problem]], [[Exploration-Exploitation Tradeoff]], [[Upper Confidence Bound Action Selection]]

## Definition

A Bayesian bandit algorithm that maintains a probability distribution over the true reward rate of each arm, samples one value from each distribution at each round, and selects the arm with the highest sample.

> [!info] Key Intuition
> Each arm has its own "belief" distribution. You pick the arm that randomly looks best this round — arms with high uncertainty sometimes win the draw and get tried. Over time, the winner's distribution narrows toward its true value.

## Algorithm (Bernoulli Bandit)

For each arm $i$ with unknown success probability $\theta_i$:

1. Maintain Beta posterior: $\theta_i \sim \text{Beta}(N_i^1 + 1,\; N_i^0 + 1)$
2. **Sample** $\hat\theta_i(n) \sim \text{Beta}(N_i^1(n)+1,\; N_i^0(n)+1)$ for each arm
3. **Select** arm $s(n) = \arg\max_i \hat\theta_i(n)$
4. **Update**: if reward = 1, increment $N_{s(n)}^1$; if 0, increment $N_{s(n)}^0$

## Intuition of the Beta Distribution

The Beta distribution is the conjugate prior for Bernoulli rewards:
- $\alpha = \beta = 1$: uniform (no information)
- Large $\alpha$, small $\beta$: concentrated near 1 (arm mostly succeeds)
- As data accumulates, the distribution narrows around the true $\theta_i$

Arms with high estimated $\theta_i$ are sampled near their true mean. Arms with high uncertainty occasionally produce extreme samples, driving exploration.

> [!example]- Worked Example
> Arm 5 has 8 successes, 2 failures → Beta(9,3), mean ≈ 0.75. Arm 7 has 1 success, 1 failure → Beta(2,2), mean = 0.5 but high variance. Thompson Sampling may sample arm 7 ≈ 0.8 this round and select it over arm 5 — giving arm 7 another chance to prove itself.

> [!warning] Common Misconception
> Thompson Sampling is not the same as UCB. UCB uses a deterministic confidence interval; Thompson Sampling is randomised. In practice, Thompson Sampling often outperforms UCB on stochastic bandits and has better empirical performance in recommendation systems.

## Significance

Thompson Sampling achieves optimal regret bounds and is state-of-the-art for Bernoulli/Gaussian bandits. It is widely used in A/B testing, recommendation engines, and clinical trials.
