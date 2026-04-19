**Tags:** #topic #hub #rl
**Related:** [[Research Papers and Innovation Trends B]], [[Proximal Policy Optimization]], [[RL Policy]], [[Reinforcement Learning]]

## Overview

This hub covers the theoretical lineage from vanilla policy gradient methods to Trust Region Policy Optimization (TRPO), establishing the principled motivation for constraining policy updates during training. The session traces how unconstrained gradient ascent on policy parameters can cause catastrophically large updates, why a natural-gradient perspective helps, and how imposing a KL divergence trust region resolves instability — setting the stage for PPO as a practical simplification.

> [!abstract]- TL;DR
> Policy gradient methods suffer from high variance and destructive large steps; TRPO (2015) introduces a KL divergence constraint that keeps each update within a "trust region" of the old policy, guaranteeing monotonic improvement. This principled but computationally heavy approach directly motivates PPO's simpler clipped surrogate objective.

## Knowledge Map

### 1. Foundations
- [[Natural Policy Gradient]]
- [[Monotonic Policy Improvement]]

### 2. Trust Region Methods
- [[Trust Region Policy Optimization]]
- [[KL Divergence Constraint in RL]]
- [[Conjugate Gradient in RL]]

### 3. Bridge to PPO
- [[Proximal Policy Optimization]]

> [!question]- Common Exam Questions
> - What is the core problem with vanilla policy gradient that motivates trust region methods?
> - State the TRPO objective function and its KL constraint. What does the constraint enforce?
> - What is the natural policy gradient and how does it differ from the vanilla policy gradient?
> - Why does TRPO use conjugate gradient instead of directly inverting the Fisher information matrix?
> - What theoretical property guarantees that TRPO does not decrease performance?
> - How does the probability ratio $r(\theta) = \pi_\theta(a|s) / \pi_{\theta_\text{old}}(a|s)$ link TRPO to PPO?
