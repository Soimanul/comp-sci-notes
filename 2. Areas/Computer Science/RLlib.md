**Tags:** #concept #rl
**Related:** [[RL Frameworks]], [[Vectorized Environments]], [[Gymnasium Environment]], [[Proximal Policy Optimization]], [[Stable Baselines3]]

## Definition

RLlib is an open-source, industry-grade reinforcement learning library built on top of Ray, designed for scalable and distributed RL training. It supports model-based, model-free, and multi-agent algorithms and is developed and maintained by Anyscale.

> [!info] Key Intuition
> RLlib solves the hard problem of parallel RL training: keeping multiple policy copies in sync across workers. By building on Ray's actor model, it makes distributed training as easy as single-machine training.

## Architecture

RLlib's API stack has three layers:

1. **Distributed Execution** — Ray Tasks and Actors (`@ray.remote`) handle parallelism
2. **Abstractions for RL** — RLlib Abstractions (Environments, Workers, Input Readers, Trainers, Policies)
3. **Application Support** — OpenAI Gym, Multi-Agent / Hierarchical, Policy Serving, Offline Data

Core abstractions:
- **Environment** (`gym.Env` or RLlib Multiagent Env): interface between agent and world
- **Trainer**: main algorithm configuration point; defines the execution plan
- **Policy**: function from state to action (contains a neural network Model)
- **Rollout Workers**: collect `(state, action, reward)` batches in parallel

## Key Features

- 32+ algorithms spanning model-based, model-free, and multi-agent settings
- Distributed implementations with multi-GPU support
- Support for major simulator APIs including Gymnasium
- TensorBoard logging and visualisation built in
- AWS and Azure cloud support
- Both TensorFlow and PyTorch as deep learning backends

## Framework Evaluation (from lecture)

| Criterion | Score |
|---|---|
| Dev. status | Active |
| Utility | High |
| Modularity | High |
| Docs | Good |
| Ecosystem | Strong |
| **Overall** | **7 / 7** |

## Distributed Training Pattern

RLlib runs $n$ parallel workers, each with a copy of the policy and a reward function, collecting batches of `(state, action, reward)`. Batches are aggregated centrally to update the policy, which is then broadcast back to all workers.

$$\max_\pi \mathbb{E}_\pi \left[ \sum_t r(s_t, a_t) \right]$$

> [!example]- Training PPO with RLlib
> ```python
> from ray.rllib.algorithms.ppo import PPOConfig
>
> config = PPOConfig().environment("CartPole-v1").rollouts(num_rollout_workers=4)
> algo = config.build()
> for _ in range(10):
>     result = algo.train()
>     print(result["episode_reward_mean"])
> ```

> [!warning] Common Misconception
> RLlib's high utility score does not mean it is the simplest choice for beginners. Its power comes with a steeper learning curve and more configuration overhead than Stable Baselines3.

## Significance

RLlib is the industry standard for RL at scale, used by AWS, Azure, and large research groups. Its hierarchical multi-agent abstractions are particularly powerful for complex cooperative or competitive scenarios.
