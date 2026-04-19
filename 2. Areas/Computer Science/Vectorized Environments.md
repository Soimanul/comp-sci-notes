**Tags:** #concept #rl
**Related:** [[RL Frameworks]], [[Gymnasium Environment]], [[Stable Baselines3]], [[RLlib]], [[Experience Replay]]

## Definition

A vectorized environment (VE) is a method for running multiple independent copies of an RL environment in parallel — typically across separate processes — so that a single agent experiences many more state transitions per unit of wall-clock time than would be possible with a single environment instance.

> [!info] Key Intuition
> Instead of collecting one experience at a time, a vectorized environment lets the agent collect $n$ experiences simultaneously — effectively multiplying sample throughput by the number of parallel workers without changing the algorithm.

## How It Works

A `VecEnv` wrapper stacks $n$ environment instances and exposes the same `reset()` / `step()` interface as a single environment, but now:

- `step(actions)` accepts a batch of $n$ actions and returns a batch of $n$ observations, rewards, dones, and infos
- Each sub-environment runs in its own process (or thread), removing the Python GIL bottleneck
- When one sub-environment reaches a terminal state, it resets automatically and continues collecting

Pseudocode:

```python
envs = make_vec_env("CartPole-v1", n_envs=8)  # 8 parallel envs
obs = envs.reset()                              # shape: (8, obs_dim)
actions = policy(obs)                           # shape: (8,)
obs, rewards, dones, infos = envs.step(actions) # batched returns
```

## Relationship to On-Policy vs Off-Policy Algorithms

- **On-policy algorithms** (e.g. PPO, A2C) benefit most from vectorized environments because they require fresh experience and cannot reuse a replay buffer. More parallel envs → larger, more diverse batches per update.
- **Off-policy algorithms** (e.g. DQN, SAC) gain less, since [[Experience Replay]] already decorrelates samples from a single environment.

> [!example]- Stable Baselines3 Usage
> ```python
> from stable_baselines3 import PPO
> from stable_baselines3.common.env_util import make_vec_env
>
> vec_env = make_vec_env("LunarLander-v2", n_envs=4)
> model = PPO("MlpPolicy", vec_env, verbose=1)
> model.learn(total_timesteps=200_000)
> ```
> With 4 parallel environments, each `learn()` step collects 4 transitions simultaneously.

> [!warning] Common Misconception
> More parallel environments do not always improve final policy quality — they increase data throughput but can introduce variance in gradient estimates. For on-policy methods there is often an optimal number of workers beyond which returns diminish.

## Significance

Vectorized environments are one of the primary practical tools for reducing wall-clock training time in deep RL. They are a standard feature in Stable Baselines3 and RLlib, and are considered a key criterion when evaluating an RL library.
