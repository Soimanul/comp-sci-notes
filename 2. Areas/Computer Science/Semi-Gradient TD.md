**Tags:** #concept #rl
**Related:** [[Approximation Methods]], [[Value Function Approximation]], [[Temporal Difference Learning]], [[Linear Function Approximation]], [[Eligibility Traces]]

## Definition

Semi-gradient TD methods apply stochastic gradient descent to minimise the value error $\overline{VE}(\mathbf{w})$, but use a **bootstrapping target** (which depends on $\mathbf{w}$) as if it were a fixed target — ignoring the gradient of the target with respect to $\mathbf{w}$. This makes them "semi" gradient methods rather than true gradient methods.

> [!info] Key Intuition
> True gradient descent treats the target as a fixed constant. Bootstrapping targets (like the TD target) shift when the weights shift — semi-gradient methods pretend they don't, which is why they can converge faster but with weaker guarantees.

## Semi-Gradient TD(0)

The prototypical semi-gradient method uses the one-step TD target $U_t = R_{t+1} + \gamma\hat{v}(S_{t+1}, \mathbf{w}_t)$:

$$\mathbf{w}_{t+1} \leftarrow \mathbf{w}_t + \alpha\left[R + \gamma\hat{v}(S', \mathbf{w}) - \hat{v}(S, \mathbf{w})\right]\nabla\hat{v}(S, \mathbf{w})$$

The gradient $\nabla\hat{v}$ is computed only with respect to the *current-state estimate*, not the next-state estimate in the target.

## Comparison to True Gradient (Monte Carlo)

| Property | Gradient MC | Semi-gradient TD |
|----------|-------------|-----------------|
| Target $U_t$ | $G_t$ (unbiased) | $R + \gamma\hat{v}(S', \mathbf{w})$ (biased) |
| Convergence guarantee | Local optimum of $\overline{VE}$ | TD fixed point (within $\frac{1}{1-\gamma}$ of optimum) |
| Learning speed | Slow (high variance) | Faster (lower variance) |
| Online/continuing use | Only episodic | Both episodic and continuing |

## N-Step Semi-Gradient TD

Extends to n-step bootstrapping targets using the n-step return $G_{t:t+n}$:

$$\mathbf{w}_{t+n} \leftarrow \mathbf{w}_{t+n-1} + \alpha\left[G_{t:t+n} - \hat{v}(S_t, \mathbf{w}_{t+n-1})\right]\nabla\hat{v}(S_t, \mathbf{w}_{t+n-1})$$

Linear semi-gradient n-step TD converges for all $n$, with error bounded within $\frac{1}{1-\gamma}$ of the optimal; the bound tightens as $n \to \infty$ (approaching MC).

> [!example]- Episodic Semi-Gradient SARSA
> For action-value control, replace $\hat{v}$ with $\hat{q}$ and use the one-step SARSA target:
> $$\mathbf{w}_{t+1} \doteq \mathbf{w}_t + \alpha\left[R_{t+1} + \gamma\hat{q}(S_{t+1}, A_{t+1}, \mathbf{w}_t) - \hat{q}(S_t, A_t, \mathbf{w}_t)\right]\nabla\hat{q}(S_t, A_t, \mathbf{w}_t)$$
> This is the natural extension of SARSA to function approximation.

> [!warning] Common Misconception
> Semi-gradient methods are not broken or approximate versions of gradient descent — they are a deliberate design choice that enables online, continuing learning with bootstrapping. Their convergence in the linear case is well-established; the issue arises only with *nonlinear* approximators under off-policy training (the deadly triad).

## Significance

Semi-gradient TD is the backbone of practical deep RL. TD(0), SARSA, Q-learning, and DQN are all semi-gradient methods. Their computational advantages (online updates, no episode boundaries needed) outweigh the weaker convergence guarantees in most applications.
