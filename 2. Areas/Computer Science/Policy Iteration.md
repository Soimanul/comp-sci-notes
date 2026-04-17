**Tags:** #concept #rl
**Related:** [[Policy Evaluation]], [[Policy Improvement Theorem]], [[Value Iteration]], [[Generalized Policy Iteration]]

## Definition

Policy Iteration alternates between full policy evaluation and greedy policy improvement until the policy stabilises. Because each improvement step yields a strictly better policy (or the optimal), convergence to $\pi_*$ is guaranteed in finite MDPs.

> [!info] Key Intuition
> Evaluate fully → improve greedily → evaluate again → improve → … Like alternating between judging how good your current plan is, then upgrading the plan, until no upgrade is possible.

## Algorithm

```
1. Initialise V(s) ∈ ℝ, π(s) ∈ A(s) arbitrarily for all s

2. Policy Evaluation — repeat:
     Δ ← 0
     For each s: v ← V(s); V(s) ← Σ_a π(a|s) Σ_{s',r} p(s',r|s,a)[r + γV(s')]; Δ ← max(Δ, |v−V(s)|)
   Until Δ < θ

3. Policy Improvement:
     policy-stable ← true
     For each s:
       old-action ← π(s)
       π(s) ← argmax_a Σ_{s',r} p(s',r|s,a)[r + γV(s')]
       If old-action ≠ π(s): policy-stable ← false
     If policy-stable: stop and return V ≈ v*, π ≈ π*; else go to 2
```

## Jack's Car Rental Example

Classic S&B example (S07): 2 locations, up to 20 cars each, Poisson arrivals/returns ($\lambda$ = 3,4 requests; 3,2 returns). Action = cars moved overnight. Starting from $\pi_0 = 0$ (move nothing), policy iteration converges to $\pi_* = $ a threshold policy in 4–5 iterations.

## Convergence

The sequence $\pi_0, \pi_1, \pi_2, \ldots$ is monotonically improving and the policy space is finite, so convergence to $\pi_*$ is guaranteed in a finite number of iterations.

> [!warning] Common Misconception
> Policy Iteration requires a **complete** evaluation sweep (until convergence) before each improvement. This is expensive — each sweep is $O(|\mathcal{S}|^2 |\mathcal{A}|)$. Value Iteration avoids this by truncating to one backup per sweep.

## Significance

Policy Iteration is the theoretical gold standard for DP planning. Its convergence proof motivates Generalised Policy Iteration, which extends to approximate, incremental, and model-free settings.
