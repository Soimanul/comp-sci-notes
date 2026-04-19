**Tags:** #concept #rl
**Related:** [[Multi-Agent Reinforcement Learning]], [[Markov Decision Process]], [[Markov Chain]]

## Definition

A Markov game (stochastic game) is the multi-agent extension of an MDP. With $N$ agents, the system state $s$ is observed by all agents simultaneously; each agent $i$ selects action $a^i$; the system transitions to a new state; and each agent $i$ receives its own reward $r^i(s, a^1, \ldots, a^N)$.

$$\langle \mathcal{S},\; \mathcal{A}^1 \times \cdots \times \mathcal{A}^N,\; T,\; R^1, \ldots, R^N \rangle$$

> [!info] Key Intuition
> A Markov game is to MARL what an MDP is to single-agent RL: the formal backbone. The critical difference is that transitions and rewards depend on the **joint action** of all agents — no single agent controls the environment alone.

## Three Game Frameworks

| Framework | Agents | Actions | Rewards | When |
|---|---|---|---|---|
| **MDP** | 1 | Sequential, solo | Single $r$ | Single-agent RL |
| **Markov Game** | $N$ | Simultaneous, joint | Per-agent $r^i$ | MARL (most settings) |
| **Extensive-form Game** | 2+ | Alternating | Terminal $r^i(z)$ | Chess, Poker, imperfect info |

In an extensive-form game, agents alternate actions and rewards are received at terminal history $z$. With imperfect information, an agent's information set is non-singleton — it cannot distinguish which node in the game tree it occupies.

## Observability and Complexity

- **Perfect information** (chess, Go): Markov game is fully observable.
- **Imperfect information** (robotics, autonomous driving): each agent receives partial observation.
- **Partially observable cooperative case**: modeled as Decentralised POMDP (Dec-POMDP) — inherently intractable in the general case.

## Non-Stationarity Problem

From any single agent's perspective, the environment is non-stationary: as other agents update their policies, transition probabilities and reward distributions change. This violates the stationary MDP assumption required for convergence guarantees of standard RL algorithms (Q-learning, policy gradient).

> [!warning] Common Misconception
> Single-agent RL algorithms applied to MARL (treating other agents as part of the environment) have no convergence guarantees. The non-stationarity introduced by co-learning agents fundamentally invalidates the MDP formulation that those algorithms rely on.

## Significance

The Markov game framework unifies MARL theory, connecting it to game-theoretic equilibrium concepts (Nash equilibrium, correlated equilibrium) and providing the formal basis for MARL algorithms (Minimax-Q, Nash-Q, CE-Q). The distinction between Markov games and extensive-form games determines whether agents act simultaneously or sequentially — a critical design choice in real-world multi-agent systems.
