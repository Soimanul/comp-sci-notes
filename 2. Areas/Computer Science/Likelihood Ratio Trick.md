**Tags:** #concept #rl
**Related:** [[Policy Gradient Theorem]], [[REINFORCE Algorithm]], [[Policy Gradient Methods]], [[Stochastic Policy Gradient]]

## Definition

The likelihood ratio trick (also called the log-derivative trick or REINFORCE trick) is an identity that converts the gradient of an expectation into an expectation of a gradient, enabling Monte Carlo estimation of policy gradients:

$$\nabla_\theta \mathbb{E}_{\tau \sim \pi_\theta}[f(\tau)] = \mathbb{E}_{\tau \sim \pi_\theta}\!\left[f(\tau)\, \nabla_\theta \ln \pi_\theta(\tau)\right]$$

For a single transition, this reduces to:

$$\frac{\nabla_\theta \pi(a|s, \theta)}{\pi(a|s, \theta)} = \nabla_\theta \ln \pi(a|s, \theta)$$

> [!info] Key Intuition
> We cannot differentiate through a stochastic sample, but we can move the gradient inside the expectation by multiplying and dividing by $\pi$ — the result is the score function $\nabla \ln \pi$, which is computable and sampleable.

## Derivation

Starting from the policy gradient theorem expression:

$$\nabla J(\theta) \propto \sum_s \mu(s) \sum_a q_\pi(s,a)\, \nabla\pi(a|s,\theta)$$

Insert $\frac{\pi(a|s,\theta)}{\pi(a|s,\theta)} = 1$:

$$= \sum_s \mu(s) \sum_a \pi(a|s,\theta)\, q_\pi(s,a)\, \frac{\nabla\pi(a|s,\theta)}{\pi(a|s,\theta)}$$

$$= \mathbb{E}_\pi\!\left[q_\pi(S_t, A_t)\, \nabla_\theta \ln\pi(A_t|S_t,\theta)\right]$$

Replacing $q_\pi(S_t, A_t)$ with the sample return $G_t$ gives the REINFORCE update.

> [!example]- Applying the Trick to a Gaussian Policy
> For $\pi(a|s,\theta) = \mathcal{N}(a;\mu_\theta(s), \sigma^2)$, we have $\ln\pi(a|s,\theta) = -\frac{(a-\mu_\theta)^2}{2\sigma^2} + \text{const}$. The score function is $\nabla_\theta \ln\pi = \frac{(a-\mu_\theta)}{\sigma^2} \nabla_\theta \mu_\theta(s)$, which pushes $\mu_\theta$ toward actions with high return.

## Significance

The likelihood ratio trick is the mathematical foundation for all Monte Carlo policy gradient estimators. It appears in REINFORCE, actor-critic updates, and variance reduction techniques, and is closely related to the score function estimator used in variational inference.
