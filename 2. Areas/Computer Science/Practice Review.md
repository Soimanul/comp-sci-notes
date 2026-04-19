**Tags:** #topic #hub #rl
**Related:** [[Reinforcement Learning]], [[Deep Q-Learning]], [[Q-Learning]], [[Proximal Policy Optimization]], [[Experience Replay]], [[Target Network]], [[State Discretization]]

## Overview

This hub covers a practice review session consolidating Deep Q-Learning techniques and comparing algorithm families across two environments: FrozenLake (solved with full DQN using PyTorch, replay buffer, and target network) and Acrobot-v1 (comparing tabular Q-Learning with state discretisation against SB3/PPO with vectorised environments).

> [!abstract]- TL;DR
> FrozenLake with DQN demonstrates the two key DQN stabilisation mechanisms — Experience Replay and Target Networks — that make deep RL training tractable. Acrobot-v1 directly contrasts tabular Q-Learning (requiring discretisation of a continuous state space) with PPO (which handles continuous states natively), illustrating when each approach is appropriate.

## Knowledge Map

### 1. FrozenLake – DQN (PyTorch)
- [[Deep Q-Learning]]
- [[Experience Replay]]
- [[Target Network]]
- [[Q-Learning]]

### 2. Acrobot-v1 – Q-Learning vs PPO
- [[Q-Learning]]
- [[State Discretization]]
- [[Proximal Policy Optimization]]
- [[Gymnasium Environment]]

### 3. Supporting Concepts
- [[Bellman Equation]]
- [[Exploration-Exploitation Tradeoff]]
- [[Epsilon-Greedy Action Selection]]

> [!question]- Common Exam Questions
> - What problem does Experience Replay solve in DQN training, and how does it work?
> - What is a Target Network, and why is it necessary for stable DQN training?
> - What is the difference between the Policy DQN and the Target DQN, and how often is the target network updated?
> - Why does tabular Q-Learning require state discretisation for Acrobot-v1, and what are the trade-offs of this approach?
> - What advantage does PPO with vectorised environments have over a single-environment tabular approach?
