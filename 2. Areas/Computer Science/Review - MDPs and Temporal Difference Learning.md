**Tags:** #hub #rl
**Related:** [[Graphs, Search, and MDPs]], [[RL Basic Concepts]], [[Dynamic Programming for RL]]

## Overview

This session consolidates MDP theory through applied problem-solving (Cat & Mouse hide-and-seek, RL maze testbed) and introduces Temporal Difference learning — the family of model-free methods that combine the online efficiency of TD bootstrapping with the empirical grounding of Monte Carlo sampling. SARSA, Q-learning, and Expected SARSA are derived and compared on the maze testbed.

> [!abstract]- TL;DR
> TD learning is model-free: it learns directly from experience without needing $p(s',r|s,a)$. SARSA is on-policy (learns the policy it follows); Q-learning is off-policy (always learns the greedy value). Expected SARSA interpolates between them. All three converge to $q_*$ under appropriate conditions.

## Knowledge Map

### 1. TD Learning Framework
- [[Temporal Difference Learning]]

### 2. TD Control Algorithms
- [[SARSA]]
- [[Q-Learning]]
- [[Expected SARSA]]

> [!question]- Common Exam Questions
> - What is the TD error and why is it called an "error"?
> - How does SARSA differ from Q-learning in its update target?
> - Why is Q-learning called "off-policy" while SARSA is "on-policy"?
> - Under what conditions does Q-learning converge?
> - In the maze testbed, why does the SARSA agent avoid dangerous states (water tiles) while Q-learning may traverse them?
