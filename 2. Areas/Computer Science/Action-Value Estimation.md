**Tags:** #concept #rl
**Related:** [[k-Armed Bandit Problem]], [[Epsilon-Greedy Action Selection]], [[Non-Stationary Rewards]]

## Definition

The problem of estimating $q_*(a)$ — the true expected reward for each action — from observed rewards, using only the history of actions taken and rewards received.

> [!info] Key Intuition
> The sample average is the statistically unbiased estimator of the mean. The incremental form makes it constant-memory and update-friendly.

## Sample-Average Method

$$Q_t(a) = \frac{\sum_{i=1}^{t-1} R_i \cdot \mathbf{1}_{A_i=a}}{\sum_{i=1}^{t-1} \mathbf{1}_{A_i=a}}$$

By the law of large numbers, $Q_t(a) \to q_*(a)$ as $N_t(a) \to \infty$.

## Incremental Update Rule

Rewriting as a running average:

$$Q_{n+1} = Q_n + \frac{1}{n}\left[R_n - Q_n\right]$$

**General form**: $\text{NewEstimate} \leftarrow \text{OldEstimate} + \alpha \left[\text{Target} - \text{OldEstimate}\right]$

This is the **error-correction** form: $R_n - Q_n$ is the prediction error; $\frac{1}{n}$ is the step size.

## Constant Step-Size for Non-Stationary Problems

Replace $\frac{1}{n}$ with a fixed $\alpha \in (0,1]$:

$$Q_{n+1} = Q_n + \alpha\left[R_n - Q_n\right] = (1-\alpha)^n Q_0 + \sum_{i=1}^n \alpha(1-\alpha)^{n-i} R_i$$

This is an **exponential recency-weighted average** — recent rewards receive weight $\alpha$, older rewards $(1-\alpha)^k \alpha$. Essential for [[Non-Stationary Rewards]].

> [!warning] Common Misconception
> The sample-average method ($\alpha = 1/n$) satisfies the stochastic approximation conditions for convergence ($\sum \alpha_n = \infty$, $\sum \alpha_n^2 < \infty$). Constant step-size does not converge — it continuously tracks a moving target, which is a feature for non-stationary problems.

## Significance

The incremental update rule is the building block of all TD learning algorithms: SARSA, Q-learning, and TD(λ) all use the same error-correction structure with different targets.
