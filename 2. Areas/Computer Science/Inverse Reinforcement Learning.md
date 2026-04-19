**Tags:** #concept #rl
**Related:** [[Advanced RL Techniques]], [[Apprenticeship Learning]], [[Reinforcement Learning]]

## Definition

Inverse Reinforcement Learning (IRL) is the problem of inferring a reward function from observed expert behaviour. Given execution traces (state-action sequences) from an agent acting optimally under some unknown reward, recover the reward function $R$ such that the expert's behaviour is optimal under that $R$.

The standard RL problem is: given $R$, find $\pi^*$. IRL is the inverse: given $\pi^*$, find $R$.

> [!info] Key Intuition
> IRL recovers *why* the expert acts the way it does — not just *what* it does. The recovered reward function then generalises to new situations in a way that mere behavioural cloning cannot, because it captures the underlying objective rather than just the surface behaviour.

## Why Infer Rewards?

The expert's reward function is often **implicit** (human preferences, biological drives) or **implicit in the environment** (physical laws, social norms). Rewards inferred via IRL:
- Generalise better to new situations than cloned behaviour
- Capture the *structure* of the task (what matters), not just the trajectory
- Enable the agent to outperform the demonstrator if the recovered reward is accurate

## Imitation Learning Comparison

| Method | Environment access | Reward learning | Interaction type |
|---|---|---|---|
| **Behavioural Cloning** | No | No | Pre-collected demos only |
| **IRL** | Yes (sim) | Yes | Pre-collected demos + RL |
| **Direct Policy Learning / Interactive IL** | Yes (interactive) | No | Live demonstrator |

## MaxEnt IRL (Ziebart et al. 2008)

Maximum Entropy IRL defines a distribution over trajectories:

$$p(\tau) = \frac{1}{Z} \exp(R_\psi(\tau))$$

where $Z = \sum_\tau \exp(R_\psi(\tau))$ is the partition function. The learning objective is to maximise the likelihood of the demonstrations:

$$\max_\psi \sum_{\tau \in \mathcal{D}} \log p_{R_\psi}(\tau)$$

The gradient has an elegant interpretation:

$$\nabla_\psi \mathcal{L} = \mathbb{E}_{\tau \sim \mathcal{D}}[\nabla_\psi R_\psi(\tau)] - \mathbb{E}_{\tau \sim \pi}[\nabla_\psi R_\psi(\tau)]$$

i.e., gradient = **demo state visitation frequencies − policy state visitation frequencies**. This leads to a simple iterative algorithm: run current policy → compute visitation discrepancy → update reward → repeat.

## Guided Cost Learning (Finn et al. ICML 2016)

GCL alternates between two steps:
1. **Sample** trajectories from the current policy
2. **Update** the reward function $R_\psi$ to increase the log-likelihood of demonstrations relative to sampled trajectories

This handles the intractable partition function in MaxEnt IRL by using importance sampling from the current policy.

## GAIL (Ho & Ermon, NIPS 2016)

Generative Adversarial Imitation Learning formulates IRL as a GAN:
- **Generator**: the policy $\pi_\theta$ (produces trajectories)
- **Discriminator**: the reward function $D_\psi$ (distinguishes expert from policy trajectories)

$$\min_\theta \max_\psi \mathbb{E}_{\tau \sim \pi_\theta}[\log D_\psi(\tau)] + \mathbb{E}_{\tau \sim \pi^*}[\log(1 - D_\psi(\tau))]$$

GAIL requires **fewer demonstrations than behavioural cloning** to achieve comparable performance, because the adversarial feedback provides a much richer training signal than supervised cross-entropy loss on a small demonstration set.

> [!example]- GAIL for Motion Capture Imitation
> GAIL was demonstrated on motion capture imitation tasks: given a few seconds of human motion capture data, the policy learns to reproduce complex locomotion skills (walking, running, cartwheel). The discriminator learns what "human motion" looks like; the policy is trained to fool it — without needing explicit reward engineering for each joint.

> [!warning] Common Misconception
> IRL does not require the demonstrator to be optimal. MaxEnt IRL assumes a *probabilistic* model where sub-optimal behaviour is possible, with probability proportional to exp(R). In practice, IRL is robust to noisy demonstrations precisely because it models a distribution over trajectories rather than assuming the demo is the unique optimal path.

## Significance

IRL is essential when the true reward function is difficult to specify manually (robotics, autonomous driving, healthcare). The connection between IRL and GANs (GAIL) unified two major streams of ML research and led directly to modern preference-learning approaches (RLHF, DPO) used to align large language models.
