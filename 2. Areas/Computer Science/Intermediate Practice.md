**Tags:** #topic #hub #rl
**Related:** [[Reinforcement Learning]], [[Q-Learning]], [[Deep Q-Learning]], [[Gymnasium Environment]], [[NEAT]], [[Proximal Policy Optimization]], [[Curriculum Learning]]

## Overview

This hub covers two parallel intermediate practice tracks: the CartPole balancing task solved with StableBaselines3 and PPO, and the IE PyRace car-driving environment solved with tabular Q-Learning and the NEAT genetic algorithm. Together they illustrate the contrast between gradient-based policy optimisation, tabular value-based methods, and evolution-based approaches on continuous-state control problems.

> [!abstract]- TL;DR
> CartPole with SB3/PPO demonstrates how framework-level RL can be applied to a classic control problem with minimal code. IE PyRace contrasts tabular Q-Learning (value-based) against NEAT (neuroevolution), with 5 short-range distance sensors as the state representation for both agents.

## Knowledge Map

### 1. CartPole + SB3/PPO
- [[Proximal Policy Optimization]]
- [[Gymnasium Environment]]
- [[RL Policy]]

### 2. IE PyRace – Q-Table Approach
- [[Q-Learning]]
- [[Action-Value Estimation]]
- [[Exploration-Exploitation Tradeoff]]

### 3. IE PyRace – NEAT Genetic Approach
- [[NEAT]]
- [[Curriculum Learning]]

### 4. Environment Design
- [[Markov Decision Process]]
- [[RL Basic Concepts]]
- [[Reward Hypothesis]]

> [!question]- Common Exam Questions
> - What is the key difference between tabular Q-Learning and NEAT as applied to the car-driving problem?
> - What does `predict_proba()` return in the SB3 context, and how does it differ from a greedy action selection?
> - Why is Curriculum Learning relevant when defining intermediate goals for a driving agent?
> - What are the 5 sensor inputs used in the PyRace environment, and why is the number of sensors reduced from a full sensor array?
> - What are the advantages and disadvantages of NEAT compared to gradient-based RL for continuous control?
