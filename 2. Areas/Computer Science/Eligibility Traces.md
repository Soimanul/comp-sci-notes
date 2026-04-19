**Tags:** #concept #rl
**Related:** [[Approximation Methods]], [[TD(λ)]], [[SARSA(λ)]], [[N-Step TD]], [[Temporal Difference Learning]], [[Semi-Gradient TD]]

## Definition

Eligibility traces are a short-term memory mechanism in reinforcement learning that records which state (or weight) components have recently been "eligible" for learning. The eligibility trace vector $\mathbf{z}_t \in \mathbb{R}^d$ parallels the long-term weight vector $\mathbf{w}_t$: when a component of $\mathbf{w}_t$ contributes to producing a value estimate, the corresponding component of $\mathbf{z}_t$ is bumped up and then decays away at rate $\gamma\lambda$.

> [!info] Key Intuition
> A TD error at time $t$ should not just update the current state — it should also update all recently visited states proportional to how recently they were visited. The eligibility trace is the mechanism that "remembers" which states are eligible to receive credit for the current TD error.

## Trace-Decay Parameter λ

The trace-decay parameter $\lambda \in [0,1]$ controls the rate at which eligibility fades:

- $\lambda = 0$: only the current state is eligible → reduces to one-step TD(0).
- $\lambda = 1$: all states remain eligible indefinitely → approximates Monte Carlo.
- Intermediate $\lambda$: a weighted blend, often better than either extreme.

The update at each step:
$$\mathbf{z}_t \leftarrow \gamma\lambda\,\mathbf{z}_{t-1} + \nabla\hat{v}(S_t, \mathbf{w}_t)$$
$$\mathbf{w}_{t+1} \leftarrow \mathbf{w}_t + \alpha\,\delta_t\,\mathbf{z}_t$$

where $\delta_t = R_{t+1} + \gamma\hat{v}(S_{t+1}, \mathbf{w}_t) - \hat{v}(S_t, \mathbf{w}_t)$ is the TD error.

## Forward View vs. Backward View

Eligibility traces give two equivalent ways to think about the same algorithm:

| View | Perspective | Computation |
|------|-------------|-------------|
| **Forward (λ-return)** | How should we update $S_t$? Look forward to all future returns, weighted by $\lambda^{n-1}$. | Requires future data; offline |
| **Backward (mechanistic)** | When TD error $\delta_t$ occurs, broadcast it backward to all eligible states. | Online, incremental; uses $\mathbf{z}_t$ |

The TD($\lambda$) algorithm implements the backward view online, empirically approximating the offline λ-return algorithm.

## Computational Advantages over N-Step Methods

- Only **one** trace vector $\mathbf{z}$ is required, rather than storing the last $n$ feature vectors.
- Learning occurs continually and uniformly in time rather than being delayed by $n$ steps.
- Updates affect behaviour *immediately* after a state is encountered rather than $n$ steps later.

> [!example]- Mountain Car with Tile Coding
> Using semi-gradient TD(λ) with tile coding on Mountain Car: with λ ≈ 0.9, the agent propagates credit back through the entire recent trajectory efficiently via the trace vector, learning a good policy several times faster than one-step TD(0) — all with constant per-step computation.

> [!warning] Common Misconception
> Eligibility traces are not simply a weighted replay of recent states. The trace vector is a *single* vector that accumulates contributions from all past states exponentially — it is computationally equivalent to but structurally different from n-step methods, which require storing $n$ explicit transitions.

## Significance

Eligibility traces unify TD and Monte Carlo methods into a single family parameterised by λ. They are one of the most computationally efficient mechanisms in RL: faster learning than one-step TD, no episode-end requirement, and $O(d)$ computation per step. They are the first line of defence against long-delayed rewards and non-Markov tasks.
