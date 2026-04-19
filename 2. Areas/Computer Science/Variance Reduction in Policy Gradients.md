**Tags:** #concept #rl
**Related:** [[REINFORCE Algorithm]], [[Baseline in Policy Gradients]], [[Advantage Function]], [[Generalized Advantage Estimation]], [[Policy Gradient Methods]]

## Definition

Variance reduction in policy gradients refers to techniques that lower the variance of the gradient estimator $\widehat{\nabla J(\theta)}$ without introducing bias (or with controlled bias), thereby accelerating and stabilising learning. High variance causes slow convergence because parameter updates point in wildly different directions across episodes.

> [!info] Key Intuition
> The raw return $G_t$ is a noisy signal: its variance grows with episode length. Any transformation that preserves the *direction* of the gradient but shrinks the *spread* of the estimator speeds up learning.

## Sources of Variance in REINFORCE

1. **Long horizons:** $G_t = \sum_{k=t}^{T}\gamma^{k-t}R_{k+1}$ accumulates noise from many future rewards.
2. **No credit assignment:** the return does not distinguish which specific actions caused the outcome.
3. **Scale sensitivity:** if all returns are large and positive, even bad actions get reinforced.

## Key Techniques

### 1. Baseline Subtraction (Unbiased)
Subtracting a state-value baseline $b(s)$ centres returns around zero. See [[Baseline in Policy Gradients]]. This is unbiased as long as the baseline does not depend on the action.

### 2. Advantage Function (Low Bias)
Replace $G_t$ with the advantage estimate $A(s,a) = Q(s,a) - V(s)$. This isolates the *relative* quality of the chosen action. See [[Advantage Function]].

### 3. Actor-Critic with TD Bootstrapping (Biased, Lower Variance)
Replace the full Monte Carlo return with a TD target $R_{t+1} + \gamma\hat{v}(S_{t+1}, \mathbf{w})$. Bootstrapping introduces bias but substantially reduces variance, often yielding faster learning. See [[Actor-Critic]].

### 4. Generalised Advantage Estimation (GAE)
GAE interpolates between the full Monte Carlo return (high variance, no bias) and the one-step TD return (low variance, high bias) using a parameter $\lambda \in [0,1]$:

$$\hat{A}_t^{\text{GAE}(\gamma,\lambda)} = \sum_{l=0}^{\infty} (\gamma\lambda)^l \delta_{t+l}$$

where $\delta_t = R_{t+1} + \gamma V(S_{t+1}) - V(S_t)$ is the TD error. See [[Generalized Advantage Estimation]].

### 5. Parameter-Based Exploration (PGPE)
Instead of sampling actions from the policy at every step, sample policy *parameters* once per episode. This provides lower-variance history samples and gradient estimates.

> [!warning] Common Misconception
> Reducing variance by adding a baseline or bootstrapping does not "improve" the policy directly — it only improves the *quality of the gradient estimate*. A lower-variance gradient still points in roughly the same direction; it just does so more reliably, enabling larger learning rates.

## Significance

Variance reduction is the central engineering challenge in policy gradient methods. Practically all modern algorithms (A2C, A3C, PPO, TRPO) pair an actor with a critic precisely because the critic provides a low-variance advantage estimate that makes policy updates tractable at scale.
