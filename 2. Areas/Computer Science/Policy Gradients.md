**Tags:** #topic #hub #rl
**Related:** [[Reinforcement Learning]], [[RL Policy]], [[Actor-Critic Methods]]

## Overview

Policy gradient methods form a family of RL algorithms that directly optimise a parameterised policy $\pi_\theta$ by ascending the gradient of a scalar performance measure $J(\theta)$. Rather than deriving a policy implicitly from an action-value function, these methods treat the policy itself as the primary object and update its parameters using gradient ascent, enabling continuous action spaces and stochastic optimal policies that value-based approaches cannot naturally represent.

> [!abstract]- TL;DR
> Policy gradient methods learn a differentiable policy directly by ascending the gradient of expected return, bypassing the need to ever compute or store action values. The Policy Gradient Theorem provides a tractable analytic gradient, and REINFORCE is the canonical Monte Carlo realisation of this idea.

## Knowledge Map

### 1. [[Policy Gradient Methods]]
- [[Stochastic Policy Gradient]]
- [[Policy Gradient Theorem]]
- [[Likelihood Ratio Trick]]

### 2. [[REINFORCE Algorithm]]
- [[Baseline in Policy Gradients]]
- [[Variance Reduction in Policy Gradients]]

### 3. Related Concepts
- [[RL Policy]]
- [[Monte Carlo Methods]]
- [[Importance Sampling]]
- [[Actor-Critic Methods]]

> [!question]- Common Exam Questions
> - What is the key update rule of REINFORCE and why is it proportional to $G_t$?
> - Why does the Policy Gradient Theorem not require the derivative of the state distribution?
> - What makes the baseline in REINFORCE valid, and what is the ideal baseline?
> - What are the three practical advantages of policy parameterisation over ε-greedy action-value methods?
> - How does the likelihood ratio trick convert the gradient of performance into an expectation?
> - Why is REINFORCE high-variance and what does adding a baseline do to the bias?
