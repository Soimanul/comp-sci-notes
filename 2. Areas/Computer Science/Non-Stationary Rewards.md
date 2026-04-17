**Tags:** #concept #rl
**Related:** [[k-Armed Bandit Problem]], [[Action-Value Estimation]], [[Epsilon-Greedy Action Selection]]

## Definition

A bandit (or RL) setting in which the true reward distributions change over time. Algorithms designed for stationary problems will fail — their estimates converge to outdated values and never re-explore previously inferior arms that have become optimal.

> [!info] Key Intuition
> In non-stationary settings, old data is misleading. You need to "forget" the past by weighting recent rewards more heavily than old ones.

## The Problem with Sample Averages

The sample-average update $Q_{n+1} = Q_n + \frac{1}{n}[R_n - Q_n]$ gives equal weight to all past rewards. If $q_*(a)$ drifts after step 500, data from steps 1–500 dilutes the signal from the true current distribution.

## Constant Step-Size Fix

Replace $\frac{1}{n}$ with fixed $\alpha$:

$$Q_{n+1} = Q_n + \alpha[R_n - Q_n]$$

This expands to an exponential recency-weighted average:

$$Q_{n+1} = (1-\alpha)^n Q_0 + \sum_{i=1}^n \alpha(1-\alpha)^{n-i} R_i$$

Weight on reward $i$ steps ago: $\alpha(1-\alpha)^{i-1}$. With $\alpha = 0.1$, a reward from 10 steps ago has weight $0.1 \times 0.9^9 \approx 0.039$ — exponentially smaller than the most recent reward.

## Optimistic Initialization Fails

Optimistic initial values encourage exploration early but are ineffective for non-stationary problems: once explored, arms are treated as known even if their distribution has since changed.

> [!warning] Common Misconception
> Constant step-size does not converge in the stochastic approximation sense — it keeps fluctuating around the true value. This is intentional: in a non-stationary world, you want the estimate to keep tracking the moving target rather than converge and stop updating.

## Significance

Most real-world RL problems are non-stationary (user preferences change, markets shift, environments evolve). The constant step-size update is the canonical fix and carries through to all TD learning algorithms.
