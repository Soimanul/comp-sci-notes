**Tags:** #topic #hub #rl
**Related:** [[Research Papers and Innovation Trends A]], [[Proximal Policy Optimization]], [[Soft Actor-Critic (SAC)]], [[Reinforcement Learning]]

## Overview

This hub covers two major threads in modern deep RL research: the detailed mechanics and practical engineering of PPO (clipped surrogate objective, GAE, optimization tricks, hyperparameter guidance, distributed variants), and the Soft Actor-Critic (SAC) algorithm family. SAC extends actor-critic methods by incorporating maximum entropy RL, where the policy simultaneously maximizes expected return and the entropy of its action distribution, yielding improved exploration and sample efficiency in continuous control. The session draws directly from the PPO paper (Schulman et al., 2017), the SAC papers (Haarnoja et al., 2018), and the discrete-action SAC extension (Christodoulou, 2019).

> [!abstract]- TL;DR
> PPO achieves TRPO-like stability through a clipped probability ratio objective, augmented with GAE, entropy regularization, and mini-batch updates — making it the practical standard for on-policy RL. SAC takes an off-policy, maximum-entropy approach that learns a stochastic policy trading off reward and entropy, making it sample-efficient and robust for continuous control and real-world robotics.

## Knowledge Map

### 1. PPO — Clipped Objective and Tricks
- [[Proximal Policy Optimization]]
- [[Entropy Regularization in RL]]

### 2. Soft Actor-Critic
- [[Soft Actor-Critic (SAC)]]
- [[Maximum Entropy RL]]
- [[Temperature Parameter in SAC]]
- [[SAC for Discrete Actions]]

> [!question]- Common Exam Questions
> - Write the PPO clipped surrogate objective $J^{\text{CLIP}}(\theta)$. What does the clip function prevent and why is a minimum taken?
> - What is Generalized Advantage Estimation (GAE) and what does the $\lambda$ parameter control?
> - Explain the role of entropy regularization in PPO. How does it affect the policy during training?
> - What does it mean for SAC to use a "maximum entropy" objective? Write the SAC policy objective.
> - Is SAC on-policy or off-policy? How does this affect its sample efficiency?
> - What is the temperature parameter $\alpha$ in SAC and what happens when $\alpha = 0$?
> - Why is the standard SAC not directly applicable to discrete action spaces? What modification is required?
> - How does the "autotuned temperature" variant of SAC work and why is manual temperature tuning problematic?
> - What is the relationship between A2C and PPO according to the Huang et al. (2022) paper?
