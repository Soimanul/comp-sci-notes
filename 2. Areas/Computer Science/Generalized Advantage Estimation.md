**Tags:** #concept #rl
**Related:** [[Advantage Function]], [[Actor-Critic]], [[Actor-Critic Methods]], [[Variance Reduction in Policy Gradients]], [[Proximal Policy Optimization]], [[Trust Region Policy Optimization]]

## Definition

Generalized Advantage Estimation (GAE, Schulman et al., 2015) is a method for computing low-variance, controllably-biased estimates of the advantage function by exponentially weighting a sum of TD errors:

$$\hat{A}_t^{\text{GAE}(\gamma, \lambda)} = \sum_{l=0}^{\infty} (\gamma\lambda)^l \delta_{t+l}$$

where $\delta_t = R_{t+1} + \gamma V(S_{t+1}) - V(S_t)$ is the one-step TD error and $\lambda \in [0,1]$ is the GAE parameter.

> [!info] Key Intuition
> GAE is the exponentially-weighted average of all $n$-step advantage estimates: $\lambda = 0$ gives the single-step TD estimate (low variance, high bias); $\lambda = 1$ gives the full Monte Carlo advantage (high variance, no bias from bootstrapping); $\lambda \in (0,1)$ smoothly interpolates between them.

## Derivation

The $n$-step advantage estimate at time $t$ is:

$$\hat{A}_t^{(n)} = -V(S_t) + \sum_{l=0}^{n-1}\gamma^l R_{t+l+1} + \gamma^n V(S_{t+n})$$

GAE is the geometric mixture of these $n$-step estimates:

$$\hat{A}_t^{\text{GAE}} = (1-\lambda)\sum_{n=1}^{\infty}\lambda^{n-1}\hat{A}_t^{(n)} = \sum_{l=0}^{\infty}(\gamma\lambda)^l\delta_{t+l}$$

In practice (finite episodes), the sum is truncated at the episode boundary.

## Special Cases

| $\lambda$ | Result |
|-----------|--------|
| $0$ | $\hat{A}_t = \delta_t = R_{t+1} + \gamma V(S_{t+1}) - V(S_t)$ (one-step TD, low variance) |
| $1$ | $\hat{A}_t = \sum_{l=0}^{\infty}\gamma^l R_{t+l+1} - V(S_t)$ (Monte Carlo advantage, unbiased) |

## Usage in Practice

GAE is the standard advantage estimator in PPO and TRPO. Typical values are $\lambda \in [0.92, 0.99]$, $\gamma \in [0.99, 0.999]$. It requires storing a trajectory of length $T$ before computing advantages, making it compatible with mini-batch gradient updates.

> [!example]- GAE in PPO
> After collecting $T$ timesteps with a policy $\pi_{\theta_\text{old}}$, PPO computes $\delta_t$ for each $t$ using the critic, then accumulates $\hat{A}_t = \delta_t + \gamma\lambda\delta_{t+1} + (\gamma\lambda)^2\delta_{t+2} + \ldots$ backwards through the trajectory. These advantages are then used to compute the clipped surrogate objective across multiple epochs of mini-batch SGD.

> [!warning] Common Misconception
> GAE does not reduce the bias from function approximation error in $V$ — it only controls the bias from bootstrapping depth. A poor critic $V$ will still produce biased advantage estimates regardless of $\lambda$.

## Significance

GAE is the dominant advantage estimation strategy in state-of-the-art policy gradient methods. It provides a single hyperparameter ($\lambda$) to control the bias–variance trade-off at training time, making it far more flexible than fixed $n$-step returns.
