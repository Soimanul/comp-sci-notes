**Tags:** #concept #rl
**Related:** [[Advanced RL Techniques]], [[Model-Based vs Model-Free RL]], [[Sim-to-Real Transfer]]

## Definition

A world model is a learned internal model of the environment that allows an agent to predict the consequences of actions without interacting with the real environment. By training a policy inside the world model ("dreaming"), the agent can learn efficiently using imagination rather than expensive real interactions.

> [!info] Key Intuition
> A world model lets the agent rehearse experience in its head: instead of taking 1 real action to get 1 data point, the agent takes 1 real action and then imagines 1,000 continuations — dramatically improving sample efficiency.

## DreamerV2 (Hafner et al. 2020)

DreamerV2 uses a **Recurrent State Space Model (RSSM)** with discrete latent representations:
- **Discrete latents**: 32 categorical variables, each with 32 classes (32×32 = 1024 bits per step)
- **World model trained separately** from actor-critic: model learns to predict observations; actor-critic learns purely inside model imagination
- **First model-based agent to achieve human-level Atari** (200M frames)

The RSSM architecture:
$$h_t = f_\phi(h_{t-1}, z_{t-1}, a_{t-1}) \quad \text{(deterministic recurrent state)}$$
$$z_t \sim q_\phi(z_t | h_t, x_t) \quad \text{(stochastic latent via encoder)}$$
$$\hat{x}_t \sim p_\phi(\hat{x}_t | h_t, z_t) \quad \text{(reconstruction decoder)}$$

## DreamerV3 (Hafner et al. 2023)

DreamerV3 is a universal world model agent with **fixed hyperparameters across all domains** (Atari, DMControl, ProcGen, Crafter, Minecraft). Key achievement: **first agent to collect diamonds in Minecraft from scratch** — a multi-step task requiring 20+ sequential tool crafting steps with extremely sparse reward.

Key contribution: robust normalization and regularization schemes that make a single set of hyperparameters work across very different reward scales and episode lengths.

## DayDreamer (Wu et al. 2022)

DayDreamer applies the Dreamer world model to **four physical robots** without any simulator:
- Quadruped learns to walk in **1 hour** of real interaction
- Uses Encoder → Decoder → Dynamics → Reward network architecture
- Key insight: world model training is constrained by **simulation throughput, not GPU compute** — the bottleneck in robotic RL is collecting real experience fast enough

> [!example]- Why Discrete Latents in DreamerV2?
> Continuous latent representations are differentiable but can collapse to posterior collapse (where the model ignores the latent entirely). Discrete categoricals (32×32 grid) avoid this: each categorical "slot" is forced to choose one of 32 discrete states, preventing the model from routing around the latent representation. The straight-through gradient estimator allows end-to-end training despite the discrete sampling.

> [!warning] Common Misconception
> World model quality ≠ rendering quality. A world model needs to accurately predict the *consequences* of actions (reward, termination, dynamics) — not to produce photorealistic reconstructions. DreamerV3 uses compact discrete latents rather than pixel-perfect reconstructions precisely because the dynamics need to be accurate, not visually realistic.

## Significance

World models reduce the sample complexity of RL from millions of real interactions to a few hundred thousand by enabling policy learning inside imagination. DreamerV3's domain generality — fixed hyperparameters across Atari, robotics, and Minecraft — suggests world models may be the path to general-purpose RL agents.
