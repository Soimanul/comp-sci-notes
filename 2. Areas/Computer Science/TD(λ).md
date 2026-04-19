**Tags:** #concept #rl
**Related:** [[Eligibility Traces]], [[Approximation Methods]], [[Temporal Difference Learning]], [[N-Step TD]], [[SARSA(λ)]], [[Semi-Gradient TD]]

## Definition

TD(λ) is one of the oldest and most widely used algorithms in reinforcement learning. It combines temporal difference learning with eligibility traces to produce a family of algorithms that interpolates between one-step TD(0) (λ=0) and Monte Carlo (λ=1). The λ-return target is:

$$G_t^\lambda \doteq (1-\lambda)\sum_{n=1}^{\infty} \lambda^{n-1} G_{t:t+n}$$

This is a geometrically weighted average of all n-step returns, normalised so the weights sum to 1.

> [!info] Key Intuition
> Instead of picking one horizon n to bootstrap at, TD(λ) takes *all* n-step returns simultaneously, weighted so that short-horizon returns count more (by factor λ) than long-horizon ones — and implements this efficiently with a single trace vector rather than storing n full trajectories.

## The λ-Return (Forward View)

The λ-return is the target of the offline λ-return algorithm. It looks *forward* from state $S_t$, weighting the $n$-step return $G_{t:t+n}$ by $(1-\lambda)\lambda^{n-1}$:

$$G_t^\lambda \doteq (1-\lambda)\sum_{n=1}^{\infty} \lambda^{n-1} G_{t:t+n}$$

- At $\lambda=0$: reduces to one-step return $G_{t:t+1}$ (TD(0)).
- At $\lambda=1$: reduces to full Monte Carlo return $G_t$.

## Semi-Gradient TD(λ) Algorithm (Backward View)

The online, incremental backward-view implementation:

```
Initialize w arbitrarily, z ← 0

Loop for each episode:
    Initialize S
    z ← 0
    Loop for each step:
        Choose A ~ π(·|S)
        Take A, observe R, S'
        z ← γλz + ∇v̂(S, w)          # accumulate trace
        δ ← R + γv̂(S', w) − v̂(S, w) # TD error
        w ← w + α δ z                  # update weights
        S ← S'
    until S' terminal
```

For linear function approximation ($\hat{v}(s,\mathbf{w}) = \mathbf{w}^\top\mathbf{x}(s)$), the trace update is $\mathbf{z} \leftarrow \gamma\lambda\mathbf{z} + \mathbf{x}(S)$.

## Three Advantages over the Offline λ-Return

TD(λ) improves over the offline λ-return algorithm in three ways:
1. Updates the weight vector on *every* step rather than only at episode end.
2. Computation is distributed equally in time, not concentrated at the end.
3. Applicable to **continuing problems** without episode boundaries.

> [!example]- λ Controls the Bias-Variance Tradeoff
> On a 19-state random walk task: λ=0 (TD) has low variance but high bias from bootstrapping; λ=1 (MC) is unbiased but high variance. Intermediate values (λ ≈ 0.7–0.9) typically achieve the best performance — the eligibility trace efficiently implements this intermediate horizon.

> [!warning] Common Misconception
> TD(λ) with λ=1 is *not* identical to Monte Carlo. The offline λ-return at λ=1 equals the MC return exactly, but semi-gradient TD(λ=1) only approximates it — it still makes online updates after every step rather than waiting for the episode to end.

## Significance

TD(λ) was the first algorithm for which a formal relationship was established between the theoretical forward view and the computationally efficient backward view. It is the conceptual foundation for True Online TD(λ), SARSA(λ), and all eligibility trace methods. Empirically, intermediate λ values significantly outperform both TD(0) and MC on tasks with long episodes or delayed rewards.
