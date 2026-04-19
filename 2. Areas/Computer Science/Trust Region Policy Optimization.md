**Tags:** #concept #rl
**Related:** [[Actor-Critic Methods]], [[Natural Policy Gradient]], [[Proximal Policy Optimization]], [[Generalized Advantage Estimation]], [[Policy Gradient Methods]], [[KL Divergence Constraint in RL]], [[Conjugate Gradient in RL]], [[Monotonic Policy Improvement]], [[Research Papers and Innovation Trends A]]

## Definition

Trust Region Policy Optimization (TRPO, Schulman et al., 2015) is a policy gradient algorithm that guarantees monotonic policy improvement by constraining each update to stay within a *trust region* — a region of parameter space where a local surrogate objective reliably approximates the true objective:

$$\max_\theta\; \mathbb{E}_t\!\left[\frac{\pi_\theta(a_t|s_t)}{\pi_{\theta_\text{old}}(a_t|s_t)}\hat{A}_t\right] \quad \text{subject to}\; \mathbb{E}_t\!\left[\text{KL}\!\left[\pi_{\theta_\text{old}}(\cdot|s_t),\,\pi_\theta(\cdot|s_t)\right]\right] \leq \delta$$

> [!info] Key Intuition
> Vanilla policy gradient steps can accidentally make the policy much worse if the step is too large. TRPO enforces a hard KL-divergence constraint so that the new policy never deviates too far from the old one, guaranteeing that performance does not collapse.

## Motivation

Standard policy gradient methods perform one gradient update per data batch and discard the data. Taking a large step risks moving into a region where the policy performs poorly, and the samples that were collected are no longer representative of the new policy. TRPO solves this by:

1. Optimising a **surrogate objective** (importance-weighted return under the old policy).
2. Constraining the update with a **KL divergence penalty** on the policy change.

This is similar to natural policy gradient methods and is theoretically justified by a bound on the performance difference between consecutive policies.

## Practical Algorithm

TRPO uses two trajectory collection strategies:
- **Single path**: collect trajectories from the current policy; use all $(s_n, a_n)$ pairs in the objective.
- **Vine**: collect trunk trajectories, then branch rollouts from selected states; common random numbers (CRN) reduce variance.

Solving the constrained optimisation requires second-order information (Fisher Information Matrix) and is implemented via conjugate gradient + line search, making TRPO computationally expensive.

## Limitations

- Requires computing (or approximating) the Fisher Information Matrix — expensive for large networks.
- Conjugate-gradient solver adds implementation complexity.
- Effective mainly for moderate-scale problems; PPO was developed as a simpler, more scalable alternative.

> [!example]- TRPO on Robotic Locomotion
> Schulman et al. demonstrated TRPO robustly learning swimming, hopping, and walking gaits for simulated robots (MuJoCo), as well as playing Atari games from pixel inputs — all with little hyperparameter tuning, due to the monotonic improvement guarantee.

> [!warning] Common Misconception
> The KL constraint in TRPO is on the *expected* KL divergence over states visited by the old policy, not the worst-case KL. In practice TRPO makes approximations that deviate from the theoretical guarantee, yet it tends to give monotonic improvement empirically.

## Significance

TRPO established the theoretical foundation for constrained policy optimisation and introduced the surrogate objective + importance sampling ratio framework. PPO subsequently approximated the TRPO constraint using clipping, achieving similar monotonic-improvement behaviour with far less computational overhead.
