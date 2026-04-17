**Tags:** #concept #rl
**Related:** [[Policy Iteration]], [[Bellman Optimality Equation]], [[Generalized Policy Iteration]], [[Dynamic Programming for RL]]

## Definition

Value Iteration updates state values using the **Bellman optimality equation** as an update rule, replacing the policy-specific Bellman backup with a max operation. It effectively performs one step of policy evaluation and policy improvement simultaneously.

$$V_{k+1}(s) \leftarrow \max_a \sum_{s',r} p(s',r|s,a)\left[r + \gamma\, V_k(s')\right]$$

> [!info] Key Intuition
> Rather than fully evaluating any single policy, Value Iteration sweeps toward $v_*$ directly by always taking the greedy best action at each update. It truncates policy evaluation to a single backup.

## Derivation from Policy Iteration

Policy Iteration's inner loop (policy evaluation) can be truncated to a single sweep without losing convergence — this is the key insight. In the extreme, one sweep = one backup = Value Iteration.

The update is the Bellman optimality operator applied repeatedly: $V_{k+1} = \mathcal{T}^* V_k$, which is a contraction (factor $\gamma$) on the space of bounded functions.

## Algorithm

```
Initialise V(s) arbitrarily; V(terminal) = 0
Repeat:
  Δ ← 0
  For each s ∈ S:
    v ← V(s)
    V(s) ← max_a Σ_{s',r} p(s',r|s,a)[r + γV(s')]
    Δ ← max(Δ, |v − V(s)|)
Until Δ < θ

Output policy: π(s) = argmax_a Σ_{s',r} p(s',r|s,a)[r + γV(s')]
```

## Policy Iteration vs Value Iteration

| | Policy Iteration | Value Iteration |
|---|---|---|
| Evaluation | Full convergence | One backup |
| Improvement | Explicit step | Embedded in update |
| Iterations | Fewer, more expensive | More, cheaper |
| Converges to | $v_* $, $\pi_*$ | $v_*$, $\pi_*$ |

In practice, value iteration often converges faster in total computation despite more sweeps.

> [!warning] Common Misconception
> Value Iteration does not maintain an explicit policy during iteration — the policy is only extracted at the end. The intermediate $V_k$ values do not correspond to any single policy's value function.

## Significance

Value Iteration is the simplest DP algorithm that directly solves for $v_*$. It is also the conceptual ancestor of Q-learning: the off-policy max target in Q-learning mirrors the max operator in Value Iteration.
