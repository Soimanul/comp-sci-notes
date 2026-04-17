**Tags:** #hub #rl
**Related:** [[RL Basic Concepts]], [[Reinforcement Learning]], [[Multi-Armed Bandits]]

## Overview

This session develops the graph-theoretic and probabilistic foundations underlying MDPs. It establishes the duality between matrices and graphs, introduces Markov chains as memoryless stochastic processes, and formalises the MDP as the canonical model for sequential decision-making. The session also presents the Bellman optimality equations and discusses the computational intractability of exact solutions for large state spaces.

> [!abstract]- TL;DR
> An MDP is a Markov chain where the agent chooses actions to influence transitions. Value functions satisfy recursive Bellman equations; solving them exactly gives the optimal policy but is intractable for large problems (e.g. $10^{20}$ states for Backgammon). All practical RL approximates the Bellman solution.

## Knowledge Map

### 1. Mathematical Foundations
- [[Markov Chain]]

### 2. The MDP Framework
- [[Markov Decision Process]]
- [[Discounted Return]]

### 3. Value Functions and Bellman Equations
- [[State Value Function]]
- [[Action Value Function]]
- [[Bellman Equation]]
- [[Bellman Optimality Equation]]

### 4. Model-Based vs Model-Free
- [[Model-Based vs Model-Free RL]]

> [!question]- Common Exam Questions
> - What is the Markov property and why is it a restriction on the state, not the decision process?
> - Write the Bellman optimality equation for $v_*$ and $q_*$.
> - Why is it computationally intractable to solve the Bellman optimality equations for most real problems?
> - What is the difference between episodic and continuing tasks, and how does the absorbing-state trick unify them?
> - How does an absorbing Markov chain relate to episodic RL tasks?
