**Tags:** #concept #rl
**Related:** [[Learning and Planning]], [[Dyna-Q]], [[Planning with a Learned Model]], [[Model-Based vs Model-Free RL]], [[Q-Learning]]

## Definition

The Dyna Architecture is a framework for integrating acting, direct reinforcement learning, model learning, and model-based planning into a single agent loop. All four processes share and update the same value function and policy.

> [!info] Key Intuition
> Real experience serves double duty: it updates the value function directly (direct RL) *and* trains the model, which then generates simulated experience for additional planning updates — multiplying the learning signal from each real step.

## Components

Dyna agents perform four concurrent activities within each time step:

1. **Acting**: select action $A$ from state $S$ using the current policy (e.g. $\varepsilon$-greedy on $Q$).
2. **Direct RL**: update $Q(S,A)$ using the real transition $(S, A, R, S')$.
3. **Model learning**: update $\text{Model}(S,A) \leftarrow R, S'$ (for a deterministic environment).
4. **Planning**: repeat $n$ times — sample a previously seen $(S,A)$, query the model for $(R,S')$, apply a Q-learning backup.

The planning step (4) is called **background planning** because it occurs between real steps and improves the policy without additional environment interaction.

> [!example]- Effect of Planning Steps $n$
> In gridworld maze experiments, a Dyna agent with $n=50$ planning steps per real step finds the optimal path in roughly 3 episodes, compared to ~25 episodes for a direct RL agent ($n=0$). Each additional simulated backup propagates value information further from the goal, accelerating convergence.

> [!warning] Model Errors
> If the environment changes after the model has been learned, the model becomes stale. Planning with an incorrect model can worsen the policy. Dyna-Q+ addresses this by adding an exploration bonus for long-unvisited state–action pairs: $r + \kappa\sqrt{\tau}$, where $\tau$ is the number of steps since the pair was last tried.

## Significance

Dyna establishes that planning and learning are not fundamentally different — both estimate value functions by backing up experience. Dyna can achieve the sample efficiency of model-based methods while remaining applicable to environments where only a learned model is available.
