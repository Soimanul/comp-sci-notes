**Tags:** #concept #rl
**Related:** [[Policy Gradients]], [[RL Policy]], [[Policy Gradient Theorem]], [[Stochastic Policy Gradient]], [[Actor-Critic Methods]]

## Definition

Policy gradient methods are RL algorithms that learn a parameterised policy $\pi(a|s, \theta)$ — where $\theta \in \mathbb{R}^{d'}$ is the policy parameter vector — by performing gradient ascent on a scalar performance measure $J(\theta)$:

$$\theta_{t+1} = \theta_t + \alpha \widehat{\nabla J(\theta_t)}$$

where $\widehat{\nabla J(\theta_t)}$ is a stochastic estimate whose expectation approximates the true gradient of $J$ with respect to $\theta_t$.

> [!info] Key Intuition
> Instead of learning *how good* each action is and inferring a policy, policy gradient methods learn the policy directly — they move the policy parameters in whatever direction increases expected return.

## How It Works

The policy can be parameterised in any way, as long as $\pi(a|s, \theta)$ is differentiable with respect to $\theta$. In practice, the policy must never become fully deterministic: $\pi(a|s,\theta) \in (0, 1)$ for all $s, a, \theta$ to ensure continued exploration.

**Soft-max parameterisation (discrete actions):** Numerical preferences $h(s, a, \theta) \in \mathbb{R}$ are computed for each state–action pair and converted to probabilities via:

$$\pi(a|s, \boldsymbol{\theta}) \doteq \frac{e^{h(s,a,\boldsymbol{\theta})}}{\sum_b e^{h(s,b,\boldsymbol{\theta})}}$$

**Gaussian parameterisation (continuous actions):** The policy outputs the mean and standard deviation of a Gaussian distribution:

$$\pi(a|s,\theta) \doteq \frac{1}{\sigma(s,\theta)\sqrt{2\pi}} \exp\!\left(-\frac{(a - \mu(s,\theta))^2}{2\sigma(s,\theta)^2}\right)$$

### Advantages over Action-Value Methods

1. **Can approach deterministic policies.** Soft-max over preferences can converge to probability 1 on a single action; ε-greedy always retains ε-random exploration.
2. **Handles stochastic optimal policies.** In imperfect-information games (e.g. Poker), the optimal policy is genuinely stochastic. Value methods cannot represent this.
3. **Policy may be simpler to approximate.** For some problems the policy is a smoother, lower-complexity function than the action-value function, yielding faster learning.
4. **Natural continuous-action handling.** Parameterising a Gaussian avoids enumerating an infinite action set.

> [!example]- Soft-Max Preferences vs. Action-Value Soft-Max
> With soft-max over *action values*, action probabilities converge to fixed non-zero probabilities determined by the relative value gaps — the policy cannot become deterministic. With soft-max over *preferences*, the preferences can grow without bound, driving one action's probability to 1. This is why preference-based parameterisation allows asymptotically deterministic behaviour.

## Significance

Policy gradient methods provide a theoretically grounded, general approach to RL that is effective in continuous action spaces, partially observable environments, and any setting where the optimal policy is stochastic. They are the foundation for REINFORCE, actor-critic, TRPO, and PPO.
