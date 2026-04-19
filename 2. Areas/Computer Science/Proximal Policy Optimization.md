**Tags:** #concept #rl
**Related:** [[RL Policy]], [[Gymnasium Environment]], [[Reinforcement Learning]], [[Actor-Critic Methods]], [[Trust Region Policy Optimization]], [[Generalized Advantage Estimation]], [[Intermediate Practice]]

## Definition

Proximal Policy Optimization (PPO) is an on-policy, policy-gradient algorithm that improves training stability by constraining each policy update to stay close to the previous policy, preventing destructively large gradient steps.

> [!info] Key Intuition
> PPO lets you take the largest possible improvement step on a policy without accidentally making it much worse — it clips the update ratio so the new policy never strays too far from the old one in a single step.

## How It Works

PPO alternates between collecting trajectory data under the current policy and performing multiple gradient-update epochs on a clipped surrogate objective:

$$L^{\text{CLIP}}(\theta) = \mathbb{E}_t\left[\min\left(r_t(\theta)\hat{A}_t,\ \text{clip}(r_t(\theta), 1-\varepsilon, 1+\varepsilon)\hat{A}_t\right)\right]$$

where $r_t(\theta) = \frac{\pi_\theta(a_t|s_t)}{\pi_{\theta_\text{old}}(a_t|s_t)}$ is the probability ratio and $\hat{A}_t$ is the estimated advantage. The clipping prevents $r_t$ from moving too far from 1, bounding how much the policy changes per update.

### Usage with StableBaselines3 (CartPole Example)

```python
from stable_baselines3 import PPO
import gymnasium as gym

env = gym.make("CartPole-v1")
model = PPO("MlpPolicy", env, verbose=1)
model.learn(total_timesteps=10_000)
```

The `predict_proba()` method (via `model.policy`) returns the probability distribution over actions for a given state, as opposed to `predict()` which returns only the greedy action.

> [!example]- CartPole Task
> CartPole: an agent must balance a pole on a cart by applying left or right forces. The state is 4-dimensional (cart position, cart velocity, pole angle, pole angular velocity). PPO with MlpPolicy learns a stable balancing policy in ~10,000 timesteps.

> [!warning] Common Misconception
> PPO is **on-policy**: each batch of experience is used for a fixed number of gradient updates and then discarded. It cannot reuse old experience (no replay buffer), unlike off-policy methods like Q-Learning or DQN. This makes sample efficiency lower but training more stable.

## Significance

PPO is one of the most widely used RL algorithms in practice (OpenAI, robotics, game AI) due to its balance of simplicity, stability, and performance. It is the default algorithm in StableBaselines3 for many benchmark environments and is directly applicable to any OpenAI-Gymnasium-compliant environment.

## From Research Papers A

**The TRPO → PPO Motivation**

The intellectual journey to PPO begins with the problem of high gradient variance in vanilla policy gradient (REINFORCE). The standard partial fix — using the advantage function $A(s,a) = Q(s,a) - V(s)$ — reduces variance but does not prevent catastrophically large parameter updates.

[[Trust Region Policy Optimization]] (Schulman et al., 2015) solved this by introducing a KL divergence hard constraint that keeps the new policy inside a trust region of the old policy. TRPO uses [[Natural Policy Gradient]] theory and [[Conjugate Gradient in RL]] to solve the constrained problem efficiently, and it is backed by the [[Monotonic Policy Improvement]] theorem.

The cost: TRPO requires two backward passes per CG iteration (Fisher-vector products) plus a backtracking line search, making it expensive and complex to implement.

PPO replaces the hard KL constraint with a soft **clip** on the probability ratio $r(\theta) = \pi_\theta(a|s)/\pi_{\theta_\text{old}}(a|s)$:

$$J^{\text{CLIP}}(\theta) = \mathbb{E}\!\left[\min\!\left(r(\theta)\hat{A}_{\theta_\text{old}}(s,a),\; \text{clip}(r(\theta), 1-\varepsilon, 1+\varepsilon)\hat{A}_{\theta_\text{old}}(s,a)\right)\right]$$

The clip function truncates $r(\theta)$ to $[1-\varepsilon, 1+\varepsilon]$ (original paper: $\varepsilon = 0.2$). The objective takes the minimum of the unclipped and clipped value, making it a pessimistic bound: the policy can only benefit from the ratio moving towards 1, not away from it. This gives TRPO-like stability using only first-order optimization.

> [!note] A2C as Special Case of PPO
> Research (Huang et al., 2022; arXiv:2205.09123) showed that A2C is a special case of PPO: when the clipped objective's clip never activates (ratio always within bounds) and GAE $\lambda = 1$, PPO reduces exactly to A2C. Empirical experiments with Stable Baselines 3 confirmed they produce identical models when other settings are controlled.

## From Research Papers B

**PPO Optimization Tricks**

The research literature identifies several practical additions beyond the base clipped objective:

- **Generalized Advantage Estimation (GAE)**: Rather than computing advantages as Reward-to-go minus $V(s)$, GAE introduces a $\lambda$ parameter that blends TD residuals across multiple timesteps ($\lambda \approx 0.95$ in SB3). TD residuals $\delta_t = r_t + \gamma V(s_{t+1}) - V(s_t)$ capture immediate impact; $\lambda$ close to 1 weights future rewards more.
- **Mini-batch Updates**: Splitting the rollout buffer into mini-batches reduces memory, adds stochastic noise that aids exploration, and pairs well with learning rate annealing.
- **Learning Rate Annealing**: Linearly decaying the learning rate over training balances fast early progress with fine-grained convergence.
- **Entropy Regularization**: Adding an entropy bonus $c_2 S[\pi_\theta](s)$ to the loss encourages exploration and prevents premature convergence.
- **Gradient Clipping**: Capping gradient norms at 0.5 prevents exploding gradients during backpropagation.
- **Approximating KL Divergence**: An approximation $\text{approx\_kl} = \mathbb{E}[(r(\theta)-1) - \log r(\theta)]$ is used as an early stopping criterion: if it exceeds $1.5 \times \text{target\_kl}$, the inner update loop breaks.

The full PPO loss with value function and entropy terms is:

$$L^{\text{CLIP+VF+S}}_t(\theta) = \hat{\mathbb{E}}_t\!\left[L^{\text{CLIP}}_t(\theta) - c_1 L^{\text{VF}}_t(\theta) + c_2 S[\pi_\theta](s_t)\right]$$

**Distributed PPO Variants**: APPO (asynchronous, multi-CPU rollout), DPPO (centralized parameter server), DD-PPO (decentralized AllReduce), and RF-DPPO (resource-flexible, separates rollout and gradient workers).

## From Actor-Critic Methods (RLI_17)

In the actor-critic framework, PPO pairs the clipped surrogate actor loss with a critic $V_\phi(s)$ that provides advantage estimates. [[Generalized Advantage Estimation]] (GAE) is the standard estimator used with PPO: the critic generates TD errors $\delta_t$, GAE combines them exponentially, and the resulting $\hat{A}_t^{\text{GAE}(\gamma,\lambda)}$ is fed into the clipped objective.

PPO (Schulman et al., 2017, arXiv:1707.06347) was specifically motivated as a simpler alternative to [[Trust Region Policy Optimization]]: TRPO's KL hard constraint requires expensive conjugate-gradient solves, while PPO's clip achieves similar monotonic-improvement behaviour with only first-order optimisation. On benchmark tasks (simulated locomotion, Atari), PPO outperforms other online policy gradient methods with better wall-time efficiency.

Relationship to A2C: PPO runs multiple parallel environments (like A2C) but performs $K$ epochs of mini-batch updates per collected batch rather than a single update — this multi-epoch data reuse is the key source of PPO's improved sample efficiency over vanilla A2C.
