**Tags:** #concept #rl
**Related:** [[Trust Region Policy Optimization]], [[Monotonic Policy Improvement]], [[Natural Policy Gradient]], [[Proximal Policy Optimization]], [[Research Papers and Innovation Trends A]]

## Definition

In the context of reinforcement learning, the KL Divergence Constraint is a hard limit on how much the probability distribution of the new policy $\pi_\theta$ may differ from the old policy $\pi_{\theta_\text{old}}$, measured by the Kullback–Leibler divergence. It serves as the mechanism that enforces the trust region in TRPO.

> [!info] Key Intuition
> KL divergence measures how "surprised" the old policy would be by the new one. Bounding it keeps the new policy in a region where the surrogate objective (computed from old-policy samples) is still a reliable approximation of the true objective.

## The Constraint

The TRPO constraint takes the form:

$$\mathbb{E}_{s \sim \pi_{\theta_\text{old}}}\!\left[D_{KL}\!\left(\pi_{\theta_\text{old}}(\cdot|s)\,\|\,\pi_\theta(\cdot|s)\right)\right] \leq \delta$$

where:
- $D_{KL}(P\|Q) = \sum_a P(a)\log\frac{P(a)}{Q(a)}$ (or integral for continuous actions)
- The expectation is over states visited under the old policy
- $\delta$ is a small positive threshold (e.g. 0.01)

### Why KL and Not $\ell_2$ Distance?

Policy parameters live in Euclidean space, but two parameter vectors that are close in $\ell_2$ may produce very different action distributions — and vice versa. KL divergence operates directly in probability distribution space, making it parameterization-invariant and directly measuring the change in agent behaviour.

### Relationship to the Probability Ratio

The KL constraint is closely related to the importance-sampling ratio used in TRPO and PPO:

$$r(\theta) = \frac{\pi_\theta(a|s)}{\pi_{\theta_\text{old}}(a|s)}$$

When $r(\theta) \approx 1$ for all $(s,a)$, the KL divergence is approximately zero. PPO enforces this informally by clipping $r(\theta)$ to $[1-\varepsilon, 1+\varepsilon]$, avoiding the need to compute KL explicitly.

> [!example]- Approximating KL in Practice
> In PPO's Stable Baselines 3 implementation, an approximate reverse KL is computed after each mini-batch update as a cheap early-stopping criterion:
> ```python
> log_ratio = log_prob - rollout_data.old_log_prob
> approx_kl_div = th.mean((th.exp(log_ratio) - 1) - log_ratio)
> if approx_kl_div > 1.5 * self.target_kl:
>     break
> ```
> This avoids computing the full KL distribution and uses the ratio-based approximation from Schulman's blog.

## Significance

The KL divergence constraint is the theoretical core of TRPO's safety guarantee. Without it, gradient ascent on the importance-weighted surrogate can take enormous steps that collapse the policy. PPO replaces the hard KL constraint with a soft clip, trading theoretical rigor for computational simplicity while achieving similar empirical stability.
