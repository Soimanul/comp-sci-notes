**Tags:** #concept #rl
**Related:** [[Actor-Critic]], [[Actor-Critic Methods]], [[Advantage Actor-Critic (A2C)]], [[Advantage Function]], [[Generalized Advantage Estimation]]

## Definition

Asynchronous Advantage Actor-Critic (A3C) is a deep RL algorithm (Mnih et al., 2016, Google DeepMind) that runs multiple independent actor-learner workers in parallel, each interacting with its own copy of the environment and asynchronously updating a shared global network.

> [!info] Key Intuition
> A3C replaces the experience replay buffer (used in DQN) with parallelism: multiple workers exploring different parts of the environment simultaneously decorrelate experience and stabilise training, without needing to store past transitions.

## Algorithm

Each worker $i$ maintains a local copy of the policy $\pi(a|s;\theta')$ and value function $V(s;\theta_v')$. It collects up to $t_{\max}$ steps (or until a terminal state), then:

1. Computes the $k$-step advantage estimate for each step $t$:
$$A(s_t, a_t; \theta, \theta_v) \approx \sum_{i=0}^{k-1}\gamma^i r_{t+i} + \gamma^k V(s_{t+k};\theta_v) - V(s_t;\theta_v)$$

2. Accumulates gradients:
$$d\theta \leftarrow d\theta + \nabla_{\theta'}\log\pi(a_t|s_t;\theta')\, A(s_t, a_t)$$
$$d\theta_v \leftarrow d\theta_v + \partial\bigl(R_t - V(s_t;\theta_v')\bigr)^2 / \partial\theta_v'$$

3. Sends accumulated gradients to the global network and updates global parameters asynchronously.
4. Pulls updated global parameters to its local copy.

## Architecture

A single global network with shared convolutional feature layers and two heads:
- **Policy head**: softmax output $\pi_\theta(a|s)$.
- **Value head**: linear output $V(s;\theta_v)$.

Workers share all non-output layers, with the policy and value heads sharing the feature representation. This sharing reduces computation and can improve generalisation.

## Key Design Choices

- **Asynchronous updates** act like parallelised SGD: different workers are at different policy versions, introducing implicit data diversity.
- **n-step returns** (rather than pure TD) balance bias and variance flexibly.
- **No replay buffer**: gradients flow directly from on-policy samples, keeping the method fully on-policy.

> [!example]- A3C vs. DQN
> DQN uses a single worker with experience replay and a target network to decorrelate data. A3C uses multiple workers in parallel environments; the diversity of their on-policy experiences achieves similar decorrelation without storing any history. A3C trained for half the wall-clock time of DQN on Atari using a multi-core CPU instead of a GPU.

> [!warning] Common Misconception
> A3C is *not* guaranteed to use fully on-policy data at any given update, since global parameters change between the time a worker copies them and the time it sends gradients back. This "staleness" is a form of off-policy learning. A2C eliminates this by synchronising all workers before updating.

## Significance

A3C (Mnih et al., 2016) demonstrated that asynchronous parallelism could replace experience replay for stabilising deep RL, and surpassed DQN on Atari while being CPU-trainable. It directly inspired A2C and established the template for parallel on-policy training used in modern large-scale RL systems.
