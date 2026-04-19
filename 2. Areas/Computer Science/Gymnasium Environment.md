**Tags:** #concept #rl
**Related:** [[Reinforcement Learning]], [[Markov Decision Process]], [[RL Basic Concepts]], [[Integration of Concepts Practice]]

## Definition

An OpenAI-Gymnasium-compliant environment is a custom simulation class that inherits from `gymnasium.Env` and implements a standardised interface (reset, step, render) so it can be used interchangeably with any Gymnasium-compatible RL library, such as StableBaselines3.

> [!info] Key Intuition
> Gymnasium is the contract between your simulation and any RL algorithm — once your environment speaks Gymnasium, you can swap Q-learning for PPO, DQN, or any other algorithm without changing the environment code.

## Mandatory Interface

A compliant environment must implement four methods:

| Method | Role |
|--------|------|
| `__init__` | Declare `self.observation_space` and `self.action_space`; initialise rendering variables |
| `reset()` | Start a new episode; called when a `done` signal is issued; returns initial observation |
| `step(action)` | Core logic: apply action, compute next state, return 5-tuple `(observation, reward, terminated, truncated, info)` |
| `render()` | Visualise the environment; supports configurable `render_modes` |

The optional `close()` method releases any open resources.

### Implementation Pattern

```python
import gymnasium as gym

class MyEnv(gym.Env):
    def __init__(self):
        self.observation_space = ...
        self.action_space = ...

    def _get_obs(self):          # private helper — call in reset & step
        ...

    def reset(self):
        ...
        return self._get_obs(), {}

    def step(self, action):
        ...
        return self._get_obs(), reward, terminated, truncated, info

    def render(self):
        ...
```

## Implementation Strategies

RL implementations exist on a spectrum of abstraction:

1. **Plain Code** — bespoke environment and agent, full control
2. **Plain Code + Custom Environment** — structured separation of env and agent
3. **Plain Code + Framework Environment** — custom env made Gymnasium-compliant (OpenAI Gymnasium)
4. **Framework Code + Framework Environment** — full framework stack (StableBaselines3)

> [!warning] Common Misconception
> The simulated environment is **not** the model. The environment defines the world the agent acts in; the model (e.g. a neural network) is the agent's policy or value function. Conflating the two leads to architectural confusion when switching RL libraries.

## Significance

Gymnasium compliance decouples environment design from algorithm choice, making it straightforward to benchmark multiple algorithms against the same environment and to use pre-built agents from StableBaselines3 (e.g. `stablebaselines3.DQN` with `CnnPolicy`).

## From RL Frameworks

The lecture (Session 13) notes that Gymnasium is the successor to OpenAI Gym, now maintained by the **Farama Foundation** — a nonprofit that also develops PettingZoo (multi-agent), Gymnasium-Robotics, Minigrid, Minari (offline RL datasets), and Shimmy (API conversion tool).

Key migration note: Gym v0.26+ → Gymnasium v0.27+ by replacing `import gym` with `import gymnasium as gym`. The current version is 1.0.0; the lecture used 0.26.0.

Most major RL libraries (ray[rllib], tf-agents, stable_baselines3, garage, acme, coach, tensorforce, tianshou, dopamine) support the Gymnasium / OpenAI Gym API, making it the de-facto standard for environment interoperability.

The Farama ecosystem of third-party environments (via `gymnasium.third-party`) covers autonomous driving (highway-env), gridworlds, robotics, multi-objective RL (MO-Gymnasium), and many-agent RL (MAgent2).
