**Tags:** #topic #hub #rl
**Related:** [[Y3S2 - Reinforcement Learning]], [[Review - MDPs and Temporal Difference Learning]]

## Overview

This hub covers temporal-difference learning — the family of model-free RL methods that combine Monte Carlo sampling (no environment model required) with dynamic programming bootstrapping (updates before episode end). It spans the one-step prediction algorithm TD(0), the three canonical TD control algorithms (SARSA, Q-learning, Expected SARSA), the maximization bias problem and its Double Q-learning fix, and the n-step bootstrapping generalisation that unifies TD(0) with Monte Carlo.

> [!abstract]- TL;DR
> TD learning is the central idea in RL: update value estimates using the Bellman equation applied to a single sampled transition rather than a full model or a full episode. Control builds on this via SARSA (on-policy), Q-learning (off-policy), Expected SARSA, and Double Q-learning; n-step TD bridges TD(0) and Monte Carlo on a single spectrum.

## Knowledge Map

### 1. TD Prediction
- [[Temporal Difference Learning]] — TD(0) update, TD error $\delta_t$, convergence guarantees, batch optimality

### 2. TD Control
- [[SARSA]] — on-policy TD control (State-Action-Reward-State-Action)
- [[Q-Learning]] — off-policy TD control, directly approximates $q_*$
- [[Expected SARSA]] — off-policy, uses expectation over policy rather than sample

### 3. Maximization Bias
- [[Maximization Bias]] — why $\max_a Q$ overestimates true values
- [[Double Q-Learning]] — two-table fix: decouple action selection from evaluation

### 4. N-Step Bootstrapping
- [[N-Step TD]] — n-step return, n-step SARSA, off-policy n-step with importance sampling

> [!question]- Common Exam Questions
> - Write the TD(0) update rule and define the TD error $\delta_t$. How does it differ from the Monte Carlo target?
> - SARSA vs Q-learning: which is on-policy, which is off-policy, and why does this matter in the cliff-walking example?
> - What is maximization bias, and how does Double Q-learning address it?
> - How does the n-step return $G_{t:t+n}$ reduce to TD(0) when $n=1$ and to Monte Carlo when $n \to \infty$?
