**Tags:** #concept #rl
**Related:** [[RL Frameworks]], [[Gymnasium Environment]], [[Reward Shaping]], [[Markov Decision Process]], [[Stable Baselines3]]

## Definition

Custom environment design is the process of formulating a real-world or simulated problem as a Markov Decision Process and implementing it as a Gymnasium-compliant environment, so that standard RL algorithms can be applied to it.

> [!info] Key Intuition
> Every RL problem requires three design decisions before writing a single line of algorithm code: what the agent can observe (observation space), what it can do (action space), and how success is measured (reward function). Getting these right matters more than which algorithm you use.

## Design Checklist

### 1. Define the MDP Components

| Component | Question to answer | Notes |
|---|---|---|
| **State / Observation** | What does the agent see at each step? | May be partial (POMDP) |
| **Action space** | Discrete (finite choices) or continuous (real-valued)? | Affects algorithm choice |
| **Reward function** | What scalar signal encodes the goal? | See [[Reward Shaping]] |
| **Episode termination** | When does an episode end? | Distinguish `terminated` vs `truncated` |
| **Initial conditions** | How is the environment reset? | Randomisation aids generalisation |

### 2. Implement the Gymnasium Interface

```python
import gymnasium as gym
from gymnasium import spaces
import numpy as np

class MyCustomEnv(gym.Env):
    metadata = {"render_modes": ["human"]}

    def __init__(self):
        super().__init__()
        self.observation_space = spaces.Box(low=-np.inf, high=np.inf,
                                            shape=(obs_dim,), dtype=np.float32)
        self.action_space = spaces.Discrete(n_actions)

    def reset(self, seed=None, options=None):
        super().reset(seed=seed)
        # initialise state
        return self._get_obs(), {}

    def step(self, action):
        # apply action, update state
        reward = self._compute_reward()
        terminated = self._is_done()
        return self._get_obs(), reward, terminated, False, {}

    def render(self): ...
    def close(self): ...
```

### 3. Common Pitfalls in Reward Design

- **Reward too sparse**: agent never receives positive feedback early in training → use [[Reward Shaping]]
- **Reward too dense**: agent exploits intermediate signals and ignores the actual goal
- **Reward scale mismatch**: mixed positive/negative signals with very different magnitudes destabilise value function learning

## Implementation Spectrum

| Level | Description |
|---|---|
| Plain code | Bespoke env + agent, full control, no reuse |
| Plain code + custom env | Structured separation but no standard API |
| Plain code + Gymnasium env | Custom env speaks the standard API; plug in any library |
| Full framework | Gymnasium env + SB3 or RLlib; maximum tooling support |

> [!example]- Worked Example: Inventory Management
> **State**: current stock level, pending orders, demand forecast
> **Actions**: discrete order quantities $\{0, 1, 2, \ldots, k\}$
> **Reward**: profit from sales minus holding cost minus stockout penalty
> **Termination**: end of planning horizon (e.g. 365 days)

> [!warning] Common Misconception
> The environment is **not** the RL model. The environment defines the world; the policy (e.g. a neural network) is what the RL algorithm learns inside that world. Confusing the two leads to architectural errors when plugging custom environments into frameworks like SB3.

## Significance

Custom environment design is the core skill that turns domain expertise into trainable RL problems. The Gymnasium standard API ensures that a well-designed custom environment is immediately compatible with any RL library — algorithm selection becomes a secondary concern once the environment is correctly specified.
