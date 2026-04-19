**Tags:** #concept #rl
**Related:** [[Approximation Methods]], [[Linear Function Approximation]], [[Tile Coding]], [[Value Function Approximation]]

## Definition

Radial Basis Functions (RBFs) are the natural generalisation of coarse coding to continuous-valued features. Rather than each feature being binary (0 or 1), an RBF feature can take any value in $[0, 1]$, reflecting the degree to which the feature is "present."

A typical Gaussian RBF feature for state $s$ with centre $c_i$ and width $\sigma_i$ is:

$$x_i(s) \doteq \exp\!\left(-\frac{\|s - c_i\|^2}{2\sigma_i^2}\right)$$

> [!info] Key Intuition
> Each RBF feature measures how close the current state is to a prototype centre — a bell-shaped activation that peaks at the centre and decays smoothly. The value function becomes a weighted sum of these Gaussian bumps.

## Properties

- **Soft boundaries**: RBFs produce smoothly varying approximations, unlike the hard tile boundaries of tile coding. This is useful when the value function is expected to vary smoothly.
- **Continuous sensitivity**: Two states close together receive similar feature vectors; distant states receive different ones — a principled notion of state similarity.
- **Linear approximation**: $\hat{v}(s, \mathbf{w}) = \mathbf{w}^\top \mathbf{x}(s)$ is still linear in $\mathbf{w}$, so all linear convergence guarantees apply.
- **Width parameter** $\sigma_i$ controls generalisation: small $\sigma$ gives narrow, sharp features (low generalisation); large $\sigma$ gives broad features (high generalisation, may oversmooth).

> [!example]- Mountain Car
> State: (position, velocity). Place RBF centres on a grid over the state space. Each feature activates strongly when the car is near that (position, velocity) centre. A smooth value function surface emerges as a weighted combination of these Gaussian features.

> [!warning] Common Misconception
> RBFs are most useful for one- or two-dimensional tasks where a smoothly varying response is important. For higher-dimensional spaces, the number of centres required grows exponentially (curse of dimensionality), making tile coding or neural networks more practical.

## Significance

RBFs provide a middle ground between hard-partition (tile coding) and fully nonlinear (neural network) approximation. They are often used in robotics and low-dimensional control tasks where smooth generalisation between states is physically motivated.
