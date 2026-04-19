**Tags:** #topic #hub #rl
**Related:** [[Introduction to Reinforcement Learning]], [[Model-Based vs Model-Free RL]], [[Q-Learning]], [[Dynamic Programming for RL]]

## Overview

This hub covers the integration of planning and learning in reinforcement learning, showing how model-based and model-free methods share a common structure centred on value-function estimation. It examines the Dyna architecture — which unifies acting, direct RL, model learning, and planning in a single agent — and explores efficient planning strategies such as prioritized sweeping and trajectory sampling. Decision-time planning approaches, including heuristic search, rollout algorithms, and Monte Carlo Tree Search, are also covered, culminating in the AlphaGo/AlphaZero case study.

> [!abstract]- TL;DR
> Both planning and learning ultimately estimate value functions by backing up simulated or real experience; the Dyna architecture exploits this to interleave acting, learning, and model-based planning in one loop. Decision-time planning methods such as MCTS focus computation on the current state at the moment of action selection.

## Knowledge Map

### 1. [[Model-Based vs Model-Free RL]]
- [[Planning with a Learned Model]]

### 2. [[Dyna Architecture]]
- [[Dyna-Q]]

### 3. Efficient Planning
- [[Prioritized Sweeping]]
- [[Trajectory Sampling]]

### 4. Decision-Time Planning
- [[Monte Carlo Tree Search]]

> [!question]- Common Exam Questions
> - What is the difference between background planning and decision-time planning?
> - Describe the Tabular Dyna-Q algorithm. Which steps correspond to direct RL, model learning, and planning?
> - How does prioritized sweeping decide which state–action pairs to update, and why is this more efficient than random sweeping?
> - What are the four phases of MCTS, and how does UCT guide node selection?
