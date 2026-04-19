**Tags:** #concept #rl
**Related:** [[Approximation Methods]], [[Deep Q-Learning]], [[Value Function Approximation]], [[Deadly Triad]], [[Experience Replay]], [[Target Network]], [[Semi-Gradient TD]]

## Definition

The Deep Q-Network (DQN) is a reinforcement learning algorithm that combines Q-learning with a deep neural network function approximator and two stabilisation mechanisms — experience replay and target networks — to make value-based deep RL stable and practical.

> [!info] Key Intuition
> DQN is what you get when you apply semi-gradient Q-learning with a neural network instead of a table: it works well enough to achieve superhuman Atari performance, but it operates squarely inside the deadly triad and requires deliberate engineering to avoid divergence.

## Architecture and Training

The Q-network $Q(s, a; \theta)$ takes a state as input and outputs Q-values for all actions simultaneously. Training minimises the mean squared Bellman error:

$$\mathcal{L}(\theta) = \mathbb{E}_{(s,a,r,s') \sim \mathcal{D}}\left[\left(r + \gamma \max_{a'} Q(s', a'; \theta^-) - Q(s, a; \theta)\right)^2\right]$$

where:
- $\mathcal{D}$ is the **replay buffer** (see [[Experience Replay]])
- $\theta^-$ are the **frozen target network** weights (see [[Target Network]])

## Key Innovations

| Innovation | Problem It Solves |
|-----------|-------------------|
| [[Experience Replay]] | Breaks temporal correlations between consecutive transitions; enables data reuse |
| [[Target Network]] | Stabilises the regression target; prevents the "chasing its own tail" divergence |

Together these two innovations make DQN the first algorithm to learn directly from high-dimensional pixel inputs across many tasks.

## Position in the RL Hierarchy

DQN is the answer when:
- State space is too large for a table (→ use VFA)
- No good hand-crafted features are available (→ use deep network, not linear VFA)

The progression: MDP → DP → MC/TD → Q-Learning/SARSA → VFA → DQN.

> [!example]- Atari Breakout
> State: 84×84 grayscale pixel stack of 4 frames. Network: convolutional neural network. Output: Q-value per discrete joystick action. The original DQN paper (Mnih et al., 2015) achieved superhuman performance on 49 Atari games from raw pixels using a single architecture and hyperparameter set.

> [!warning] Common Misconception
> DQN does not solve the deadly triad — it operates inside it. The target network and replay buffer *reduce* instability empirically but do not provide the theoretical convergence guarantees that on-policy linear methods have. DQN can and does diverge on some tasks.

## Significance

DQN launched the era of deep RL by demonstrating that neural network Q-learning, with the right stabilisation tricks, can solve complex tasks end-to-end from raw observations. It established experience replay and target networks as standard components of value-based deep RL.
