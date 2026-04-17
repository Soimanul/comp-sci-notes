**Tags:** #concept #rl
**Related:** [[Reinforcement Learning]], [[State Value Function]], [[Policy Evaluation]], [[Policy Iteration]]

## Definition

A policy $\pi$ is a mapping from states to probabilities over actions. It defines the agent's complete behaviour: given state $s$, $\pi(a|s)$ gives the probability of selecting action $a$.

> [!info] Key Intuition
> The policy is the agent's strategy — everything the agent has learned about how to act is encoded in $\pi$.

## Types of Policies

**Deterministic policy**: $\pi(s) = a$ — maps each state to a single action.

**Stochastic policy**: $\pi(a|s) \in [0,1]$ — maps each state to a distribution over actions, with $\sum_a \pi(a|s) = 1$.

**Greedy policy**: $\pi(s) = \arg\max_a Q(s,a)$ — always selects the highest-valued action.

**ε-greedy policy**: greedy with probability $1-\varepsilon$; uniform random with probability $\varepsilon$.

## Policy Evaluation vs. Policy Improvement

- **Policy evaluation**: given $\pi$, compute $v_\pi$ (how good is this policy?)
- **Policy improvement**: given $v_\pi$, find a better policy $\pi'$

These two operations alternate in [[Policy Iteration]] and underlie all of [[Generalized Policy Iteration]].

> [!example]- Worked Example
> In a gridworld, an ε-greedy policy with ε=0.1: at state $s$, the agent moves to the highest-value adjacent cell 90% of the time; 10% of the time it picks a random direction (north/south/east/west uniformly). This ensures all states remain reachable during training.

> [!warning] Common Misconception
> A deterministic optimal policy always exists for finite MDPs (the greedy policy w.r.t. $v_*$). You never need a stochastic policy at optimality — stochastic policies are needed during learning for exploration.

## Significance

The policy is the primary object RL seeks to optimise. All value-based methods compute value functions to derive a better policy; policy gradient methods directly parameterise and optimise $\pi$.
