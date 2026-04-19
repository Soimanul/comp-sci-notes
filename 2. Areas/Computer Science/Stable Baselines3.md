**Tags:** #concept #rl
**Related:** [[RL Frameworks]], [[Gymnasium Environment]], [[Vectorized Environments]], [[Logging and Monitoring RL]], [[Proximal Policy Optimization]]

## Definition

Stable Baselines3 (SB3) is a set of reliable, PyTorch-based implementations of reinforcement learning algorithms. It is the successor to Stable Baselines (originally built on TensorFlow) and is developed under the DLR-RM organisation.

> [!info] Key Intuition
> SB3 trades raw customisability for correctness: every algorithm has been tested against published benchmarks, so you can trust the implementation and focus on environment design and hyperparameter tuning.

## Key Features

- Unified code structure across all algorithms (PEP8 compliant, clean code)
- Documented functions and classes; high test coverage with type hints
- Built-in TensorBoard integration for training curves
- Native support for [[Vectorized Environments]] (multiprocess training)
- Companion tool **RL Baselines3 Zoo** (`rl-baselines3-zoo`): pre-trained agents, training scripts, hyperparameter tuning, plotting, and video recording
- **SB3 Contrib**: experimental/latest algorithms not yet in the main library

## Supported Algorithms

SB3 supports algorithms including A2C, DDPG, DQN, HER, PPO, SAC, and TD3. All share a common `learn()`, `predict()`, and `save()`/`load()` API.

## Framework Evaluation (from lecture)

| Criterion | Score |
|---|---|
| Dev. status | Active |
| Utility | Low |
| Modularity | Medium |
| Docs | Good |
| Ecosystem | Medium |
| **Overall** | **4.5 / 7** |

> [!example]- Minimal Training Loop
> ```python
> from stable_baselines3 import PPO
> import gymnasium as gym
>
> env = gym.make("LunarLander-v2")
> model = PPO("MlpPolicy", env, verbose=1)
> model.learn(total_timesteps=100_000)
> model.save("ppo_lunarlander")
> ```

> [!warning] Common Misconception
> SB3's "Low" utility score reflects its relatively small number of algorithms compared to RLlib — not a flaw in the implementations themselves. For prototyping a single algorithm, SB3 is often the fastest starting point precisely because of its simplicity.

## Significance

SB3 is the go-to library for single-machine, single-agent RL experimentation and teaching. Its Gymnasium compatibility means any custom environment can be plugged in directly, and the Zoo companion provides a hyperparameter search pipeline out of the box.
