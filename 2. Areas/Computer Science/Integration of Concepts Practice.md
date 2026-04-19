**Tags:** #topic #hub #rl
**Related:** [[Reinforcement Learning]], [[Q-Learning]], [[Bellman Equation]], [[Deep Q-Learning]], [[Gymnasium Environment]]

## Overview

This hub covers the first integration practice for reinforcement learning concepts, centred on the Snake game as a worked environment. It brings together environment design, state representation, reward shaping, agent architecture, and algorithm selection — including Deep Q-Learning, genetic algorithms, and non-ML search techniques — and concludes with a comparison of implementation strategies using OpenAI Gymnasium.

> [!abstract]- TL;DR
> The Snake game is used as a unifying environment to compare RL approaches (Deep Q-Learning, genetic algorithms, shortest-path search, Hamiltonian cycle) across dimensions of performance, generality, and computational cost. Building an OpenAI-Gymnasium-compliant environment is the standard bridge between custom simulations and framework-level RL libraries like StableBaselines3.

## Knowledge Map

### 1. [[Reinforcement Learning]]
- [[RL Basic Concepts]]
- [[Reward Hypothesis]]
- [[Markov Decision Process]]

### 2. [[Deep Q-Learning]]
- [[Q-Learning]]
- [[Bellman Equation]]
- [[Action Value Function]]
- [[Exploration-Exploitation Tradeoff]]

### 3. [[Gymnasium Environment]]
- [[Model-Based vs Model-Free RL]]
- [[RL Policy]]

### 4. Non-ML Baselines (Snake)
- Shortest-path search (Dijkstra / A*)
- Hamiltonian Cycle (unbeatable, NP complexity)
- Genetic algorithms applied to Snake

> [!question]- Common Exam Questions
> - What is the Bellman equation update rule used in Deep Q-Learning, and what role does the discount factor γ play?
> - What are the four mandatory methods of an OpenAI-Gymnasium-compliant environment?
> - Why is the Hamiltonian Cycle approach guaranteed to beat Snake, and what is its computational complexity class?
> - What are the trade-offs between TD DQN and a shortest-path algorithm when applied to Snake?
> - Why does expanding the agent's vision (beyond 4-directional danger flags) dramatically increase state-space size?
