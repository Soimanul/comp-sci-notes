**Tags:** #concept #rl
**Related:** [[Deep Q-Learning]], [[Q-Learning]], [[Target Network]], [[Approximation Methods]], [[Deadly Triad]], [[Practice Review]]

## Definition

Experience Replay is a DQN training mechanism in which agent transitions $(s, a, r, s')$ are stored in a fixed-size **replay buffer** and sampled randomly to form training mini-batches, rather than learning directly from consecutive experience.

> [!info] Key Intuition
> Neural networks trained on sequential data suffer because consecutive steps are highly correlated — the network keeps updating on almost identical examples. Replaying random past transitions breaks this correlation and reuses data efficiently.

## How It Works

At each timestep, the agent:
1. Executes action $a_t$ in state $s_t$, receives $r_t$ and observes $s_{t+1}$
2. Stores transition $(s_t, a_t, r_t, s_{t+1})$ in the replay buffer $\mathcal{D}$ (FIFO queue of fixed capacity, e.g. 10,000)
3. Samples a random mini-batch of transitions from $\mathcal{D}$
4. Computes Bellman targets using the sampled batch
5. Performs a gradient update on the Q-network using the mini-batch loss

$$\mathcal{L}(\theta) = \mathbb{E}_{(s,a,r,s') \sim \mathcal{D}}\left[\left(r + \gamma \max_{a'} Q(s', a'; \theta^-) - Q(s, a; \theta)\right)^2\right]$$

where $\theta^-$ are the **target network** weights (see [[Target Network]]).

> [!example]- FrozenLake Context
> In FrozenLake DQN training, each step the agent stores the (state, action, reward, next_state, done) tuple. Once the buffer has enough samples (e.g. >1,000), random mini-batches of size 64 are drawn for each gradient step. This means the agent may learn from a transition it experienced 500 steps ago, preventing the network from overfitting to the most recent trajectory.

> [!warning] Common Misconception
> Experience Replay makes DQN **off-policy** in practice, even though the original Q-learning update is off-policy by design. The mini-batch contains transitions from potentially very different behaviour policies (early random exploration vs. later trained policy). This is fine for Q-learning because Q-learning is off-policy, but it is incompatible with on-policy algorithms like PPO, which must discard old experience.

## Significance

Experience Replay, combined with Target Networks, is one of the two key innovations in DeepMind's original DQN paper (2015) that made deep RL stable on Atari. It improves sample efficiency and reduces variance in gradient estimates, both critical for training deep networks on RL objectives.

## From Approximation Methods

Experience Replay addresses the **off-policy training** arm of the [[Deadly Triad]]: because the replay buffer contains transitions from many past policies (early random exploration through later trained behaviour), DQN learns off-policy by design. This is compatible with Q-learning but incompatible with on-policy methods such as SARSA or PPO. In the broader context of [[Value Function Approximation]], replay also converts the highly correlated online data stream into an approximately i.i.d. mini-batch — a prerequisite for stable SGD with neural network approximators.
