**Tags:** #concept #rl
**Related:** [[Policy Gradient Methods]], [[Policy Gradient Theorem]], [[Likelihood Ratio Trick]], [[REINFORCE Algorithm]], [[RL Policy]]

## Definition

A stochastic policy gradient is the gradient of the expected return $J(\theta) = \mathbb{E}_\pi[G_0]$ with respect to the parameters $\theta$ of a stochastic policy $\pi_\theta$. The update rule performs gradient ascent:

$$\theta_{t+1} = \theta_t + \alpha \widehat{\nabla J(\theta_t)}$$

where $\widehat{\nabla J(\theta_t)}$ is an unbiased or low-bias estimate obtained by sampling trajectories from $\pi_\theta$.

> [!info] Key Intuition
> A stochastic policy maps each state to a *distribution* over actions; its gradient tells us how to shift that distribution to increase expected reward.

## Why Stochastic Policies

Stochastic policies are essential in three scenarios:

1. **Exploration**: a non-zero probability on all actions allows the agent to discover better strategies.
2. **Partial observability**: when the observation does not uniquely determine the best action, randomising can be optimal.
3. **Imperfect information games**: mixed (stochastic) strategies are Nash-optimal in games like Poker.

## Gradient Estimate

By the [[Policy Gradient Theorem]] and [[Likelihood Ratio Trick]]:

$$\widehat{\nabla J(\theta)} = G_t\, \nabla_\theta \ln\pi(A_t|S_t, \theta)$$

The term $\nabla_\theta \ln\pi(A_t|S_t, \theta)$ is called the **eligibility vector** — it is the direction in parameter space that most increases the log-probability of repeating action $A_t$ in state $S_t$.

The update scales this direction by the return $G_t$: high-return actions get reinforced, low-return actions are suppressed, and the division by $\pi$ corrects for the sampling frequency of each action.

> [!warning] Common Misconception
> Stochastic policies are not merely an exploration heuristic — they are sometimes the *optimal* policy (e.g. in POMDPs and game theory). A deterministic policy is a special case where the distribution collapses to a point mass.

## Significance

The stochastic policy gradient framework generalises Q-learning to parameterised policies, works naturally in continuous action spaces, and provides the foundation for all modern deep RL policy optimisation methods.
