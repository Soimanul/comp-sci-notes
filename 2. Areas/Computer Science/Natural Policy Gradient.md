**Tags:** #concept #rl
**Related:** [[Trust Region Policy Optimization]], [[Actor-Critic Methods]], [[Proximal Policy Optimization]], [[Policy Gradient Methods]], [[Research Papers and Innovation Trends A]]

## Definition

The Natural Policy Gradient is a policy optimization method that preconditions the standard gradient by the inverse of the Fisher information matrix, yielding an update direction that is invariant to the parameterization of the policy and measures steepest ascent in the space of probability distributions rather than parameter space.

> [!info] Key Intuition
> Ordinary gradient descent treats all parameter directions equally, but the Fisher matrix tells you the local curvature of the policy's distribution — the natural gradient re-scales the step so that equal movement in distribution space corresponds to equal movement in parameter space.

## How It Works

The vanilla policy gradient is:

$$\nabla J(\theta) = \mathbb{E}_{\pi_\theta}\left[\nabla_\theta \log \pi_\theta(a|s)\, \hat{A}(s,a)\right]$$

The natural policy gradient replaces this with:

$$\tilde{\nabla} J(\theta) = F(\theta)^{-1} \nabla J(\theta)$$

where $F(\theta)$ is the Fisher information matrix:

$$F(\theta) = \mathbb{E}_{\pi_\theta}\left[\nabla_\theta \log \pi_\theta(a|s)\, \nabla_\theta \log \pi_\theta(a|s)^\top\right]$$

Premultiplying by $F^{-1}$ makes the update invariant to how the policy is parameterized: a re-parameterization that stretches parameter space does not change the natural gradient update in policy space.

Computing $F^{-1}$ exactly is infeasible for large neural networks (it is $d \times d$ where $d$ is the number of parameters), which is why TRPO approximates the Fisher-vector product and uses conjugate gradient to solve $F\,x = g$ without explicitly forming $F^{-1}$.

> [!example]- Comparison with Vanilla Gradient
> Suppose a policy has two parameters: one that barely changes the distribution and one that drastically changes it. Vanilla gradient descent would treat both equally, potentially taking a huge step in distribution space via the sensitive parameter. The natural gradient would automatically dampen the sensitive direction and amplify the insensitive one, giving a balanced update in policy distribution space.

## Significance

The natural policy gradient is the theoretical foundation for TRPO and, by extension, PPO. It is also used in K-FAC-based optimizers (Kronecker-Factored Approximate Curvature), which approximate the Fisher matrix efficiently for large networks, making second-order RL optimization tractable.
