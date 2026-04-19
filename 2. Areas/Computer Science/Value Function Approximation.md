**Tags:** #concept #rl
**Related:** [[Approximation Methods]], [[State Value Function]], [[Temporal Difference Learning]], [[Semi-Gradient TD]], [[Linear Function Approximation]]

## Definition

Value Function Approximation (VFA) replaces the tabular value function $V(s)$ or $Q(s,a)$ with a parameterised function $\hat{v}(s, \mathbf{w}) \approx v_\pi(s)$, where $\mathbf{w} \in \mathbb{R}^d$ is a weight vector with far fewer components than there are states ($d \ll |S|$).

> [!info] Key Intuition
> Updating one weight changes the estimated value of *many* states simultaneously — this generalisation is what makes approximation powerful enough to handle state spaces that are too large to enumerate.

## The Prediction Objective (VE)

Because we cannot make every state's estimate accurate simultaneously, we must specify which states matter most via a state distribution $\mu(s)$. The **Value Error** objective is:

$$\overline{VE}(\mathbf{w}) \doteq \sum_{s \in \mathcal{S}} \mu(s)\left[v_\pi(s) - \hat{v}(s, \mathbf{w})\right]^2$$

In the on-policy case, $\mu(s)$ is the fraction of time spent in state $s$ under the current policy — the on-policy distribution.

## Training via Stochastic Gradient Descent

Each prediction update $s \mapsto u$ becomes a supervised training example with input $s$ and target $u$. The general SGD update is:

$$\mathbf{w}_{t+1} \doteq \mathbf{w}_t + \alpha\left[U_t - \hat{v}(S_t, \mathbf{w}_t)\right] \nabla\hat{v}(S_t, \mathbf{w}_t)$$

- If $U_t = G_t$ (MC return): **true gradient descent**, guaranteed to converge to a local optimum.
- If $U_t = R_{t+1} + \gamma\hat{v}(S_{t+1}, \mathbf{w}_t)$ (TD target): **semi-gradient**, not true gradient descent because the target depends on $\mathbf{w}_t$.

> [!example]- Semi-Gradient TD(0) Update
> At each step, compute the TD target $U_t = R_{t+1} + \gamma\hat{v}(S_{t+1}, \mathbf{w})$, then update:
> $$\mathbf{w} \leftarrow \mathbf{w} + \alpha\left[R + \gamma\hat{v}(S', \mathbf{w}) - \hat{v}(S, \mathbf{w})\right]\nabla\hat{v}(S, \mathbf{w})$$
> The gradient $\nabla\hat{v}$ is computed with respect to $\mathbf{w}$ only at the *current* state — the effect of $\mathbf{w}$ on the *target* is ignored, making this "semi" gradient.

> [!warning] Common Misconception
> Having fewer weights than states does not mean the approximator is inaccurate — it means updating one weight *generalises* to many states. But this generalisation is also a liability: improving accuracy at one state may inadvertently worsen it at others.

## Significance

VFA is the bridge from tabular RL to scalable deep RL. The framework applies to any differentiable function class — linear models, neural networks, decision trees — and the same SGD principle drives everything from linear semi-gradient TD to DQN.
