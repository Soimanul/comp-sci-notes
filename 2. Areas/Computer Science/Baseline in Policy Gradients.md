**Tags:** #concept #rl
**Related:** [[REINFORCE Algorithm]], [[Variance Reduction in Policy Gradients]], [[Policy Gradient Theorem]], [[State Value Function]], [[Advantage Function]]

## Definition

A baseline $b(s)$ is a state-dependent (but action-independent) function subtracted from the return inside the policy gradient update:

$$\theta_{t+1} \doteq \theta_t + \alpha\bigl(G_t - b(S_t)\bigr)\frac{\nabla\pi(A_t|S_t, \boldsymbol{\theta}_t)}{\pi(A_t|S_t, \boldsymbol{\theta}_t)}$$

The baseline can be any function that does not vary with the action — including a random variable — without introducing bias into the gradient estimate.

> [!info] Key Intuition
> A baseline centres the return signal: actions that exceed the baseline are reinforced, and actions that fall short are suppressed. Without a baseline, even mediocre actions get reinforced if the return happens to be large.

## Why the Baseline Leaves the Gradient Unbiased

The generalised policy gradient theorem establishes:

$$\nabla J(\boldsymbol{\theta}) \propto \sum_s \mu(s) \sum_a \bigl(q_\pi(s,a) - b(s)\bigr)\nabla\pi(a|s,\boldsymbol{\theta})$$

The subtracted term $b(s)$ integrates to zero because $\sum_a \nabla\pi(a|s,\theta) = \nabla \sum_a \pi(a|s,\theta) = \nabla 1 = 0$. Hence the baseline drops out of the expectation, leaving the gradient unchanged.

## Choosing the Baseline

The baseline should vary with state: states where all actions have high values need a high baseline to distinguish the best action; states with uniformly low values need a low baseline.

**Natural choice:** the estimated state value $\hat{v}(S_t, \mathbf{w})$, learned by a parallel Monte Carlo or TD method with weight vector $\mathbf{w}$. The resulting update:

$$\delta_t = G_t - \hat{v}(S_t, \mathbf{w})$$
$$\mathbf{w} \leftarrow \mathbf{w} + \alpha^\mathbf{w}\,\delta_t\,\nabla\hat{v}(S_t, \mathbf{w})$$
$$\boldsymbol{\theta} \leftarrow \boldsymbol{\theta} + \alpha^\theta\,\gamma^t\,\delta_t\,\nabla\ln\pi(A_t|S_t, \boldsymbol{\theta})$$

Note the two separate step sizes $\alpha^\theta$ and $\alpha^\mathbf{w}$ (hyperparameters).

> [!example]- Gradient Bandit as Special Case
> In the gradient bandit algorithm, the baseline is the running average reward $\bar{R}$. This is analogous: the update reinforces actions that beat average, suppresses those that do not. Adding a state-dependent baseline to REINFORCE is the same idea extended to the full MDP setting.

> [!warning] Common Misconception
> REINFORCE with baseline is *not* an actor-critic method. The state-value function is used only as a baseline for the current state's return — it is not used for bootstrapping (updating from the next state's estimated value). Bootstrapping is what distinguishes actor-critic from REINFORCE with baseline.

## Significance

The baseline is the primary tool for variance reduction in policy gradient methods. It is a prerequisite for practical REINFORCE and the conceptual bridge to actor-critic, where the critic provides a bootstrapped baseline rather than a Monte Carlo one.
