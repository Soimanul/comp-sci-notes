**Tags:** #concept #rl
**Related:** [[Policy Gradient Methods]], [[Policy Gradients]], [[REINFORCE Algorithm]], [[Likelihood Ratio Trick]], [[Action Value Function]]

## Definition

The Policy Gradient Theorem gives an analytic expression for the gradient of the performance measure $J(\theta)$ with respect to the policy parameter $\theta$, for the episodic case:

$$\nabla J(\boldsymbol{\theta}) \propto \sum_s \mu(s) \sum_a q_\pi(s, a) \nabla \pi(a|s, \boldsymbol{\theta})$$

where $\mu(s)$ is the on-policy state distribution (the fraction of time spent in each state under $\pi$) and $q_\pi(s, a)$ is the true action-value function.

> [!info] Key Intuition
> The gradient of performance depends only on the gradient of the policy and the action values — it does not require differentiating through the environment's state distribution, which is generally unknown.

## Why It Matters

With ε-greedy selection, action probabilities can change dramatically for an arbitrarily small change in estimated action values (if a different action becomes maximal). With continuous policy parameterisation, action probabilities change *smoothly* as a function of $\theta$, enabling stronger convergence guarantees.

The theorem is significant because computing $\nabla J(\theta)$ naively would require knowing how the state distribution $\mu(s)$ changes with $\theta$ — which depends on the full environment dynamics. The theorem shows that this derivative drops out: the gradient can be expressed purely in terms of quantities we can estimate from samples.

## Deriving the Estimator

The theorem implies that $\nabla J(\theta)$ equals (up to a normalising constant):

$$\mathbb{E}_\pi\!\left[\sum_a q_\pi(S_t, a) \nabla\pi(a|S_t, \boldsymbol{\theta})\right]$$

Applying the [[Likelihood Ratio Trick]] (i.e. multiplying and dividing by $\pi(a|S_t, \theta)$) converts this sum over all actions into a single sampled action:

$$\nabla J(\boldsymbol{\theta}) \propto \mathbb{E}_\pi\!\left[G_t \frac{\nabla \pi(A_t|S_t, \boldsymbol{\theta})}{\pi(A_t|S_t, \boldsymbol{\theta})}\right] = \mathbb{E}_\pi\!\left[G_t \nabla \ln \pi(A_t|S_t, \boldsymbol{\theta})\right]$$

This expectation can be estimated by sampling trajectories, yielding the [[REINFORCE Algorithm]].

> [!warning] Common Misconception
> The theorem holds for the on-policy distribution $\mu$ — estimates must be collected under the current policy $\pi_\theta$. Using off-policy data without importance-sampling corrections breaks the gradient estimate.

## Significance

The Policy Gradient Theorem is the theoretical backbone of all policy-gradient methods. It establishes that gradient ascent in $J$ is tractable without a differentiable environment model, and it directly motivates REINFORCE, actor-critic, and their modern descendants (TRPO, PPO).
