**Tags:** #hub #rl
**Related:** [[Reinforcement Learning]], [[Introduction to Reinforcement Learning]], [[Exploration-Exploitation Tradeoff]]

## Overview

The k-armed bandit problem is the simplest form of the RL problem: a single state, $k$ actions, and evaluative (stochastic) rewards. It isolates the exploration-exploitation tradeoff without the complications of sequential state transitions. This session covers the family of bandit algorithms from simple greedy baselines through UCB, gradient bandits, Thompson Sampling, and the extension to contextual bandits as a bridge to full RL.

> [!abstract]- TL;DR
> Bandit algorithms must balance exploring uncertain arms and exploiting known good arms. UCB achieves this principally by tracking uncertainty; Thompson Sampling uses Bayesian posteriors; gradient bandits learn action preferences directly. All outperform pure greedy under stationary rewards; non-stationary rewards require constant step-size updates.

## Knowledge Map

### 1. Problem Formulation
- [[k-Armed Bandit Problem]]
- [[Action-Value Estimation]]
- [[Non-Stationary Rewards]]

### 2. Action Selection Methods
- [[Epsilon-Greedy Action Selection]]
- [[Upper Confidence Bound Action Selection]]
- [[Gradient Bandit Algorithm]]
- [[Thompson Sampling]]

### 3. Extensions
- [[Contextual Bandits]]

> [!question]- Common Exam Questions
> - What is the difference between a stationary and non-stationary bandit, and how does the update rule change?
> - Derive the incremental update formula $Q_{n+1} = Q_n + \frac{1}{n}[R_n - Q_n]$.
> - Why does UCB outperform ε-greedy by selecting exploration targets more intelligently?
> - What is the role of the baseline $\bar{R}_t$ in the gradient bandit update?
> - How does a contextual bandit differ from both a standard bandit and full RL?
