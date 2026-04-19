**Tags:** #concept #rl
**Related:** [[Maximum Entropy RL]], [[Entropy Regularization in RL]], [[Temperature Parameter in SAC]], [[SAC for Discrete Actions]], [[Experience Replay]], [[Target Network]], [[Research Papers and Innovation Trends B]]

## Definition

Soft Actor-Critic (SAC) is an off-policy, model-free, actor-critic deep RL algorithm based on the maximum entropy RL framework (Haarnoja et al., 2018). It trains a stochastic policy to maximize the expected discounted sum of rewards and policy entropy simultaneously, yielding strong sample efficiency and stability on continuous control tasks.

> [!info] Key Intuition
> SAC is an actor-critic that treats exploration not as a heuristic add-on but as part of the objective itself — the critic values both reward and entropy, so the actor is intrinsically incentivized to "succeed at the task while acting as randomly as possible."

## How It Works

### Objective

$$\pi^* = \arg\max_\pi \; \mathbb{E}\!\left[\sum_{t=0}^{\infty} \gamma^t \left(R(s_t, a_t, s_{t+1}) + \alpha\, H(\pi(\cdot|s_t))\right)\right]$$

The temperature $\alpha$ controls the trade-off between reward and entropy. When $\alpha = 0$, SAC collapses to standard expected-return maximization.

### Architecture

SAC maintains the following networks:

| Component | Role |
|---|---|
| **Actor** $\pi_\phi(a|s)$ | Stochastic policy network; outputs action distribution |
| **Critic 1** $Q_{\theta_1}(s,a)$ | Main Q-network |
| **Critic 2** $Q_{\theta_2}(s,a)$ | Second Q-network (clipped double-Q trick from TD3) |
| **Target Critics** $Q_{\bar\theta_1}, Q_{\bar\theta_2}$ | Slowly updated targets for stable Bellman targets |
| **Replay Buffer** | Off-policy experience storage |

The critics learn soft Q-values where entropy is included in the Bellman target. The actor improves by maximizing the soft Q-value minus entropy cost. The critics are updated using the minimum of the two Q-networks (clipped double-Q) to avoid overestimation.

### Key Properties

- **Off-policy**: uses a replay buffer, so data from past policies is reused — high sample efficiency.
- **Stochastic policy**: unlike DDPG/TD3, the actor outputs a distribution (reparameterization trick with squashed Gaussian), not a deterministic action.
- **Stable**: inherits target policy smoothing from the stochasticity of the policy, without needing explicit noise injection.
- **Continuous action space**: the original SAC formulation assumes continuous actions. See [[SAC for Discrete Actions]] for the discrete extension.

> [!example]- SAC in Robotics
> SAC was validated on real-world robotic tasks (quadrupedal locomotion, dexterous hand manipulation) by the Berkeley AI Research group. It achieved state-of-the-art performance with far fewer environment interactions than on-policy methods like PPO, making it practical for physical robots where data collection is expensive.

> [!warning] Common Misconception
> Despite using an importance ratio-like mechanism, SAC is **not** related to PPO's importance sampling. SAC's off-policy nature comes from the replay buffer and the maximum entropy Q-learning formulation — not from reweighting trajectories. The two algorithms have entirely different update mechanisms.

## Significance

SAC is the leading off-policy algorithm for continuous control, outperforming both on-policy (PPO) and other off-policy (TD3, DDPG) methods in sample efficiency on MuJoCo benchmarks. Its combination of stability, sample efficiency, and robustness to hyperparameters (especially in the autotuned-temperature variant) makes it the algorithm of choice for real-world robotics. It is available in Stable Baselines 3 for continuous action environments.
