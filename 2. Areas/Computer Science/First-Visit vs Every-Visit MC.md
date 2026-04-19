**Tags:** #concept #rl
**Related:** [[Monte Carlo Prediction]], [[Monte Carlo Methods]], [[State Value Function]]

## Definition

Two variants of Monte Carlo prediction that differ in which visits to a state $s$ within an episode are used to update the value estimate:

- **First-visit MC**: averages the returns following the **first** time state $s$ is visited in each episode.
- **Every-visit MC**: averages the returns following **all** visits to $s$ across all episodes.

> [!info] Key Intuition
> First-visit MC treats each episode as a single independent observation of $s$; every-visit MC squeezes more data per episode but introduces mild correlations between the returns used.

## Algorithm — First-Visit MC Prediction

```
Input: policy π to evaluate
Initialise V(s) arbitrarily for all s; Returns(s) ← empty list

Loop forever (each episode):
  Generate episode following π: S₀, A₀, R₁, ..., S_{T-1}, A_{T-1}, R_T
  G ← 0
  Loop for t = T-1, T-2, ..., 0:
    G ← γG + R_{t+1}
    Unless S_t appears in S₀, S₁, ..., S_{t-1}:
      Append G to Returns(S_t)
      V(S_t) ← average(Returns(S_t))
```

Every-visit MC is identical except the check `Unless S_t appears earlier` is removed.

## Convergence Properties

| | First-Visit MC | Every-Visit MC |
|---|---|---|
| Convergence | Converges to $v_\pi(s)$ as visits $\to \infty$ | Converges to $v_\pi(s)$ as visits $\to \infty$ |
| Bias | Unbiased | Biased (but consistent) |
| Theoretical study | Studied since 1940s; more established | Extends to function approximation and eligibility traces |
| Practical preference | Standard in tabular settings | Preferred with function approximation |

> [!example]- Example: Multiple Visits in One Episode
> Suppose state $s$ is visited at $t=2$ (return $G_2 = 5$) and again at $t=5$ (return $G_5 = 2$) in the same episode.
> - First-visit MC appends only $G_2 = 5$ to $\text{Returns}(s)$.
> - Every-visit MC appends both $G_2 = 5$ and $G_5 = 2$ to $\text{Returns}(s)$.

> [!warning] Common Misconception
> The returns $G_2$ and $G_5$ from the same episode are not independent (they share overlapping reward sequences). This is why every-visit MC introduces bias, even though it still converges asymptotically.

## Significance

The choice rarely matters in practice — both converge to the correct value. However, first-visit MC has cleaner theoretical properties for tabular problems, while every-visit MC is the natural choice when extending to approximate methods with eligibility traces (Sutton & Barto, Chapter 12).
