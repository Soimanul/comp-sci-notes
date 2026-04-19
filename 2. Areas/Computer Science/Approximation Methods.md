**Tags:** #topic #hub #rl
**Related:** [[Reinforcement Learning]], [[Temporal Difference Learning]], [[N-Step TD]], [[Eligibility Traces]]

## Overview

When state spaces become combinatorially large, tabular RL methods are no longer viable — storing and updating one value per state is impractical, and almost every state encountered is brand new. This hub covers the approximate solution methods that extend TD and MC methods to arbitrarily large state spaces by representing value functions as parameterised functions rather than tables. The four pillars are on-policy prediction with approximation, on-policy control with approximation, off-policy methods with approximation, and eligibility traces.

> [!abstract]- TL;DR
> Approximate solution methods replace lookup tables with function approximators (linear, neural) and update their parameters using semi-gradient descent. Combining function approximation with bootstrapping and off-policy training creates the "deadly triad" instability; eligibility traces (TD(λ)) efficiently interpolate between TD and MC.

## Knowledge Map

### 1. On-Policy Prediction with Approximation
- [[Value Function Approximation]]
- [[Linear Function Approximation]]
- [[Tile Coding]]
- [[Radial Basis Functions]]
- [[Semi-Gradient TD]]

### 2. On-Policy Control with Approximation
- [[SARSA]]
- [[Semi-Gradient TD]]

### 3. Off-Policy Methods with Approximation
- [[Deadly Triad]]
- [[Deep Q-Network (DQN)]]

### 4. Eligibility Traces
- [[Eligibility Traces]]
- [[TD(λ)]]
- [[SARSA(λ)]]

### 5. Deep RL with Approximation
- [[Deep Q-Learning]]
- [[Experience Replay]]
- [[Target Network]]

> [!question]- Common Exam Questions
> - What is the value error (VE) objective and why is it weighted by the on-policy distribution μ(s)?
> - What are the three components of the deadly triad, and why does removing any one of them avoid divergence?
> - How does semi-gradient TD(0) differ from true gradient descent, and when does each converge?
> - Explain the forward view (λ-return) and backward view (eligibility traces) of TD(λ) and describe their equivalence.
