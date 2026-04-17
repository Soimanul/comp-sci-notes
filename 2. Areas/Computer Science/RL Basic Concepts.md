**Tags:** #hub #rl
**Related:** [[Introduction to Reinforcement Learning]], [[Reinforcement Learning]]

## Overview

This session formalises the agent-environment interaction using Markov Decision Processes (MDPs) and introduces the mathematical machinery — states, actions, rewards, dynamics, returns, and value functions — that underpins all of RL theory. It also positions MDPs on the spectrum from fully-observable to partially-observable environments (POMDPs).

> [!abstract]- TL;DR
> MDPs provide the canonical formal framework for RL: the agent selects actions given states, the environment responds with rewards and next states according to the dynamics function $p(s',r|s,a)$. Value functions summarise expected future reward and are the central objects all RL algorithms seek to estimate or optimise.

## Knowledge Map

### 1. The MDP Framework
- [[Markov Decision Process]]
- [[Markov Chain]]

### 2. Returns and Discounting
- [[Discounted Return]]
- [[Reward Hypothesis]]

### 3. Value Functions
- [[State Value Function]]
- [[Action Value Function]]
- [[Bellman Equation]]
- [[Bellman Optimality Equation]]

### 4. Partial Observability
- [[Model-Based vs Model-Free RL]]

> [!question]- Common Exam Questions
> - Write the Bellman equation for $v_\pi(s)$.
> - What is the Markov property and why does it matter for MDPs?
> - What is the difference between $v_\pi$ and $q_\pi$?
> - How does discounting convert a continuing task into a tractable optimisation problem?
> - Why is a POMDP harder than a fully-observable MDP?
