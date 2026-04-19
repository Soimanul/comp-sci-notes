**Tags:** #concept #rl
**Related:** [[Policy Gradients]], [[Policy Gradient Theorem]], [[Likelihood Ratio Trick]], [[Baseline in Policy Gradients]], [[Variance Reduction in Policy Gradients]], [[Monte Carlo Methods]]

## Definition

REINFORCE (Williams, 1992) is a Monte Carlo policy-gradient control algorithm that updates the policy parameters $\theta$ after each complete episode using the observed return $G_t$:

$$\theta_{t+1} \doteq \theta_t + \alpha \gamma^t G_t \nabla \ln\pi(A_t|S_t, \boldsymbol{\theta}_t)$$

where $G_t = \sum_{k=t+1}^{T} \gamma^{k-t-1} R_k$ is the discounted return from time $t$, and $\gamma^t$ accounts for the general discounted case.

> [!info] Key Intuition
> REINFORCE increases the log-probability of actions that led to high returns and decreases it for low-return actions — proportionally to how much better or worse the outcome was than chance.

## Algorithm

```
Input: differentiable policy π(a|s, θ), step size α > 0
Initialise θ ∈ ℝ^d' (e.g. to 0)

Loop forever (each episode):
  Generate episode S₀, A₀, R₁, …, S_{T-1}, A_{T-1}, R_T following π(·|·, θ)
  For each step t = 0, 1, …, T−1:
    G ← Σ_{k=t+1}^{T} γ^{k-t-1} R_k
    θ ← θ + α γ^t G ∇ln π(A_t|S_t, θ)
```

The term $\nabla \ln\pi(A_t|S_t, \boldsymbol{\theta})$ is the **eligibility vector** — it points in the direction that most increases the probability of repeating $A_t$ in $S_t$.

## Intuition Behind the Update

Each increment to $\theta$ is proportional to:
- $G_t$: the return. This ensures parameters move most in directions that favoured high-return actions.
- $\frac{\nabla\pi(A_t|S_t,\theta)}{\pi(A_t|S_t,\theta)}$: the inverse of the action probability. This corrects for frequency: actions sampled often would otherwise dominate updates even if they are mediocre.

> [!example]- Episode Walkthrough
> Suppose in state $s$ the agent takes action $a$ with probability 0.3, receives a high return $G_t = 10$. The update adds $10 \cdot \frac{\nabla\pi(a|s,\theta)}{0.3}$ to $\theta$, strongly reinforcing $a$. If a different action with probability 0.9 gave $G_t = 2$, its update $2 \cdot \frac{\nabla\pi}{0.9}$ is much smaller — the rarer, higher-return action wins.

> [!warning] Common Misconception
> REINFORCE is a **Monte Carlo** method: it uses the *complete* return from time $t$ to the episode end. All parameter updates happen *after* the episode completes, making it undefined for continuing (non-episodic) tasks. It is also high-variance because $G_t$ is a noisy estimate of $q_\pi(s,a)$.

## Significance

REINFORCE is the canonical on-policy Monte Carlo policy gradient algorithm. Despite its high variance, it converges to a local optimum of $J(\theta)$ under standard stochastic approximation conditions. It is the direct predecessor of REINFORCE with baseline and actor-critic methods.
