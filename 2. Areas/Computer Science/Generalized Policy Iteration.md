**Tags:** #concept #rl
**Related:** [[Policy Evaluation]], [[Policy Improvement Theorem]], [[Policy Iteration]], [[Value Iteration]]

## Definition

Generalised Policy Iteration (GPI) is the general principle that any RL algorithm can be viewed as an interleaving of policy evaluation (making $V$ consistent with $\pi$) and policy improvement (making $\pi$ greedy with respect to $V$), regardless of granularity or order.

> [!info] Key Intuition
> GPI is the unifying framework of all value-based RL: evaluation pushes $V$ toward $v_\pi$; improvement pushes $\pi$ toward greedy w.r.t. $V$. These two forces compete but ultimately stabilise at the fixed point $\pi = \pi_*$, $V = v_*$.

## The GPI Diagram

```
π ──── Evaluation ────▶ V(s)
▲                         |
└────── Improvement ──────┘
```

- **Evaluation pull**: $V \to v_\pi$ (given fixed $\pi$)
- **Improvement pull**: $\pi \to \text{greedy}(V)$ (given fixed $V$)

These goals conflict (improvement changes $\pi$, invalidating $V$), but the interplay converges to a fixed point where $v_\pi = v_*$ and $\pi$ is greedy w.r.t. $v_\pi = v_*$.

## Examples of GPI Instances

| Algorithm | Evaluation granularity | Improvement granularity |
|---|---|---|
| Policy Iteration | Full sweep to convergence | Full sweep after evaluation |
| Value Iteration | Single backup per state | Implicit (embedded in update) |
| SARSA | One TD step | Implicit (ε-greedy selection) |
| Q-learning | One TD step | Off-policy max target |
| Actor-Critic | Continuous TD updates | Continuous policy gradient steps |

> [!warning] Common Misconception
> GPI does not require that evaluation fully converges before improvement occurs, or vice versa. TD methods perform both simultaneously at every step. What matters is that both processes are active and consistent — neither can be entirely absent.

## Significance

GPI is the most important organising concept in RL theory. It shows that policy evaluation and improvement are sufficient (and necessary) to reach optimality, regardless of how they are interleaved.

## From Monte Carlo Methods

Monte Carlo control follows the GPI schema but replaces the model-dependent Bellman backup with averaging sampled returns. Policy evaluation estimates $q_\pi$ from episodes; policy improvement is greedy w.r.t. the estimated $Q$ table. The key difference from DP GPI: evaluation and improvement are interleaved episode-by-episode rather than sweep-by-sweep, and no transition model $p(s',r|s,a)$ is needed. See [[Monte Carlo Control]].
