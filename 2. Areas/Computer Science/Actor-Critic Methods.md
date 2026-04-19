**Tags:** #topic #hub #rl
**Related:** [[Reinforcement Learning]], [[Policy Gradients]], [[Proximal Policy Optimization]]

## Overview

Actor-critic methods extend policy gradient methods by pairing a learned policy (the **actor**) with a learned value function (the **critic**). The critic evaluates the actor's choices using bootstrapped TD estimates, providing a low-variance learning signal that makes continuous, online updates possible — unlike pure Monte Carlo methods such as REINFORCE, which must wait until the episode ends.

> [!abstract]- TL;DR
> Actor-critic methods combine the best of policy gradients (direct policy optimisation) and value-based methods (bootstrapped value estimates): the critic replaces the full Monte Carlo return with a TD signal, drastically reducing variance while the actor uses that signal to improve the policy step by step.

## Knowledge Map

### 1. [[Actor-Critic]]
- [[Advantage Function]]
- [[Advantage Actor-Critic (A2C)]]
- [[Asynchronous Advantage Actor-Critic (A3C)]]

### 2. Advanced Methods
- [[Generalized Advantage Estimation]]
- [[Trust Region Policy Optimization]]
- [[Natural Policy Gradient]]
- [[Proximal Policy Optimization]]

### 3. Foundations
- [[Policy Gradients]]
- [[Baseline in Policy Gradients]]
- [[Variance Reduction in Policy Gradients]]
- [[Temporal Difference Learning]]

> [!question]- Common Exam Questions
> - What distinguishes an actor-critic method from REINFORCE with baseline? (Answer: bootstrapping.)
> - Write the one-step actor-critic update for both the actor and critic parameters.
> - What is the advantage function and why is it preferred over the raw action-value as the critic signal?
> - How does A3C differ from A2C in terms of parallelism and gradient accumulation?
> - What problem does TRPO solve that vanilla policy gradient does not, and how does PPO approximate the same constraint?
> - Define GAE and explain the role of $\lambda$ in the bias–variance trade-off.
> - What is the natural gradient and why does it converge faster than the ordinary gradient for policy optimisation?
