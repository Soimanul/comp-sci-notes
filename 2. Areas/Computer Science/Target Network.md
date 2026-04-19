**Tags:** #concept #rl
**Related:** [[Deep Q-Learning]], [[Experience Replay]], [[Q-Learning]], [[Bellman Equation]], [[Approximation Methods]], [[Deadly Triad]], [[Practice Review]]

## Definition

A Target Network is a periodically frozen copy of the Q-network used exclusively to compute Bellman training targets in DQN. It is distinct from the **online (policy) network**, whose weights are updated every gradient step.

> [!info] Key Intuition
> Training a neural network where the target keeps changing every step is like trying to hit a moving bullseye — the network chases its own tail. Freezing the target for a fixed number of steps gives stable learning objectives, making training converge.

## How It Works

DQN maintains two networks with the same architecture:

| Network | Symbol | Role | Update frequency |
|---------|--------|------|-----------------|
| Policy (online) network | $\theta$ | Selects actions; trained by gradient descent | Every step |
| Target network | $\theta^-$ | Computes Bellman targets only | Every $C$ steps (hard copy) or via soft update |

The Bellman target used during training is:

$$y_t = r_t + \gamma \max_{a'} Q(s_{t+1}, a'; \theta^-)$$

The loss minimised is $(y_t - Q(s_t, a_t; \theta))^2$. Because $\theta^-$ is frozen, $y_t$ is a stationary target for $C$ steps.

**Hard update**: every $C$ gradient steps, copy $\theta \to \theta^-$ exactly.
**Soft update** (Polyak averaging): $\theta^- \leftarrow \tau\theta + (1-\tau)\theta^-$ at every step, with $\tau \ll 1$.

> [!example]- FrozenLake DQN Training
> Online network weights $\theta$ are updated at every mini-batch gradient step. The target network $\theta^-$ is copied from $\theta$ every 100 steps. During those 100 steps the Bellman target $y_t = r + \gamma \max_{a'} Q(s', a'; \theta^-)$ is stable, preventing the "deadly triad" of function approximation + bootstrapping + off-policy data from causing divergence.

> [!warning] Common Misconception
> The target network is **not** a second agent or a different policy. Both networks share the same architecture and represent $Q(s,a)$. The target network is simply a lagged copy of the online network used solely to stabilise the regression target — it never directly selects actions during training.

## Significance

Target Networks are one of the two key stabilisation mechanisms (alongside [[Experience Replay]]) in DeepMind's original DQN. Without a frozen target, bootstrapped Q-learning updates with a neural network approximator tend to diverge because the target and the estimate are coupled — improving one worsens the other in a feedback loop.

## From Approximation Methods

In the language of the [[Deadly Triad]], the target network addresses the **bootstrapping** arm: by freezing $\theta^-$, the Bellman target $y_t = r + \gamma\max_{a'}Q(s',a';\theta^-)$ becomes a stationary regression target for $C$ steps, making the learning problem temporarily equivalent to supervised regression. This prevents the positive feedback loop that arises when both the target and the estimate are updated by the same gradient step — a loop that is particularly dangerous when combined with off-policy data and a nonlinear function approximator ([[Value Function Approximation]]).
