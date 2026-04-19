**Tags:** #concept #rl
**Related:** [[Dynamic Programming for RL]], [[Bellman Equation]], [[Policy Iteration]], [[RL Policy]]

## Definition

Policy Evaluation (the **prediction** problem) computes the state-value function $v_\pi$ for a given policy $\pi$ by iteratively applying the Bellman equation as an update operator until convergence.

> [!info] Key Intuition
> Starting from any initial $V_0$, repeatedly applying the Bellman backup brings the estimates closer to $v_\pi$ on each sweep — like propagating information backward from known terminal rewards through the state space.

## Iterative Update

For each state $s \in \mathcal{S}$, repeatedly apply:

$$V_{k+1}(s) \leftarrow \sum_a \pi(a|s) \sum_{s',r} p(s',r|s,a)\left[r + \gamma\, V_k(s')\right]$$

Terminate when $\Delta = \max_s |V_{k+1}(s) - V_k(s)| < \theta$ (small threshold).

## Algorithm (from S&B)

```
Initialise V(s) arbitrarily for all s; V(terminal) = 0
Repeat:
  Δ ← 0
  For each s ∈ S:
    v ← V(s)
    V(s) ← Σ_a π(a|s) Σ_{s',r} p(s',r|s,a)[r + γV(s')]
    Δ ← max(Δ, |v - V(s)|)
Until Δ < θ
```

## Convergence

The sequence $V_0, V_1, V_2, \ldots$ converges to $v_\pi$ for any initial $V_0$ (with $V(\text{terminal}) = 0$), provided $\gamma < 1$ or all states eventually reach a terminal state. Convergence is guaranteed by the contraction mapping theorem.

> [!example]- Worked Example
> Gridworld 4×4, $\gamma=1$, uniform random policy. After one sweep, states adjacent to goal get $V = -1$. After two sweeps, states two steps away get $V \approx -2$. After ~100 sweeps the estimates stabilise at the expected number of steps to the goal.

> [!warning] Common Misconception
> Policy evaluation does NOT find the optimal policy — it evaluates a given, fixed policy. To find $\pi_*$, you need to follow it with policy improvement (→ Policy Iteration) or use Value Iteration directly.

## Significance

Policy evaluation is the "E step" in the GPI cycle. It is also the basis for Monte Carlo and TD prediction methods, which estimate $v_\pi$ without requiring the model $p$.

## From Monte Carlo Methods

Monte Carlo prediction is the model-free alternative to iterative DP policy evaluation. Rather than computing $v_\pi(s)$ via Bellman backups, MC simply averages the actual returns $G_t$ observed after visiting $s$ under policy $\pi$. No transition model is required. The tradeoff: MC must wait for complete episodes before updating, whereas DP can update after a single step using the model. Both first-visit and every-visit MC converge to $v_\pi(s)$. See [[Monte Carlo Prediction]] and [[First-Visit vs Every-Visit MC]].
