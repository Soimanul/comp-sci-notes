**Tags:** #concept #rl
**Related:** [[Actor-Critic Methods]], [[Policy Gradient Methods]], [[Advantage Function]], [[Baseline in Policy Gradients]], [[Temporal Difference Learning]], [[State Value Function]]

## Definition

An actor-critic method is a policy gradient algorithm in which two components are learned simultaneously:

- **Actor**: the parameterised policy $\pi(a|s, \theta)$ that selects actions.
- **Critic**: a parameterised value function $\hat{v}(s, \mathbf{w})$ that evaluates the actor's choices by computing a TD error $\delta_t$.

The critic's TD error serves as the reinforcement signal for the actor, replacing the high-variance Monte Carlo return used in REINFORCE.

> [!info] Key Intuition
> The critic "criticises" the actor's action selection using a predicted value of the next state — it does not wait until the episode ends to judge whether an action was good.

## Why Actor-Critic is Different from REINFORCE with Baseline

REINFORCE with baseline also learns a state-value function alongside the policy, but uses it only as a baseline for the Monte Carlo return $G_t$. The value function is **not** used for bootstrapping.

In actor-critic methods, the state-value function is applied to the *second* state of the transition ($S_{t+1}$), forming the one-step return:

$$G_{t:t+1} = R_{t+1} + \gamma\hat{v}(S_{t+1}, \mathbf{w})$$

This is bootstrapping: the value of the next state is used to estimate the value of the current action. This introduces bias but substantially reduces variance.

## One-Step Actor-Critic Update

$$\delta_t = R_{t+1} + \gamma\hat{v}(S_{t+1}, \mathbf{w}) - \hat{v}(S_t, \mathbf{w})$$

**Critic update** (semi-gradient TD(0)):
$$\mathbf{w} \leftarrow \mathbf{w} + \alpha^\mathbf{w}\,\delta_t\,\nabla\hat{v}(S_t, \mathbf{w})$$

**Actor update:**
$$\boldsymbol{\theta} \leftarrow \boldsymbol{\theta} + \alpha^\theta\,I\,\delta_t\,\nabla\ln\pi(A_t|S_t, \boldsymbol{\theta})$$

where $I = \gamma^t$ is a discount factor that de-emphasises later time steps in the episode ($I \leftarrow \gamma I$ each step).

This is a **fully online, incremental** algorithm: states, actions, and rewards are processed as they occur and never revisited.

## Baseline Summary (Common Forms)

| Critic Signal | Algorithm |
|---|---|
| $G_t$ (full return) | REINFORCE |
| $Q^w(s,a)$ | Q Actor-Critic |
| $A^w(s,a) = Q^w(s,a) - V^w(s)$ | Advantage Actor-Critic |
| $\delta_t$ (TD error) | TD Actor-Critic |

> [!example]- Q Actor-Critic Algorithm
> Initialize $s, \theta, w$; sample $a \sim \pi_\theta(a|s)$. For each step: sample $r \sim R(s,a)$, $s' \sim P(s'|s,a)$, $a' \sim \pi_\theta(a'|s')$. Update actor: $\theta \leftarrow \theta + \alpha_\theta Q_w(s,a)\nabla_\theta\ln\pi_\theta(a|s)$. Compute TD error: $\delta = r + \gamma Q_w(s',a') - Q_w(s,a)$. Update critic: $w \leftarrow w + \alpha_w \delta \nabla_w Q_w(s,a)$. Advance: $a \leftarrow a'$, $s \leftarrow s'$.

> [!warning] Common Misconception
> The bias in the actor-critic gradient estimate is not due to bootstrapping *per se* — even if the critic were learned by a Monte Carlo method, the actor would still be biased because the function approximation is imperfect. Bootstrapping is used because it reduces variance, not because it removes bias.

## Significance

Actor-critic methods are the foundation of the modern deep RL landscape: A2C, A3C, PPO, TRPO, SAC, and DDPG are all actor-critic variants. Their key advantage is fully online learning compatible with both episodic and continuing problems, with a flexible bias–variance trade-off controlled by the bootstrapping depth.
