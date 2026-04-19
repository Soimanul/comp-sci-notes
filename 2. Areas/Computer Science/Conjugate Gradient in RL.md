**Tags:** #concept #rl
**Related:** [[Trust Region Policy Optimization]], [[Natural Policy Gradient]], [[KL Divergence Constraint in RL]], [[Research Papers and Innovation Trends A]]

## Definition

Conjugate Gradient in RL refers to the application of the iterative conjugate gradient (CG) algorithm to solve the linear system $Fx = g$ that arises in TRPO, where $F$ is the Fisher information matrix and $g$ is the policy gradient. It allows computing the natural gradient direction $F^{-1}g$ without ever forming or inverting $F$ explicitly.

> [!info] Key Intuition
> Directly computing $F^{-1}$ costs $O(d^2)$ memory and $O(d^3)$ time for a network with $d$ parameters — completely infeasible. Conjugate gradient only requires the ability to compute Fisher-vector products $Fv$ for arbitrary vectors $v$, which can be done in $O(d)$ time via two backpropagation passes.

## How It Works

TRPO approximates the KL constraint with a quadratic:

$$D_{KL}(\pi_{\theta_\text{old}} \| \pi_\theta) \approx \frac{1}{2}(\theta - \theta_\text{old})^\top F (\theta - \theta_\text{old})$$

The constrained update then reduces to solving:

$$F\,x = g, \quad \text{where } g = \nabla_\theta J(\theta)$$

and setting $\Delta\theta = \alpha \cdot x$ with step size $\alpha$ found by backtracking line search.

### Fisher-Vector Product

The key trick is that for a policy parameterized by $\theta$:

$$Fv = \nabla_\theta\!\left[(\nabla_\theta \log \pi_\theta)^\top v\right]$$

This can be computed by:
1. Computing $u = \nabla_\theta \log \pi_\theta$ (one backward pass).
2. Computing $u^\top v$ (dot product).
3. Back-propagating through $u^\top v$ with respect to $\theta$ (second backward pass).

This gives $Fv$ in $O(d)$ — the same cost as a gradient computation.

> [!example]- Conjugate Gradient Iterations
> In practice, TRPO runs only 10 conjugate gradient iterations (not until full convergence). This gives a good enough approximation of $F^{-1}g$ at low cost, after which a backtracking line search checks that the KL constraint is satisfied before accepting the step.

## Significance

Conjugate gradient makes TRPO computationally feasible for neural networks: it avoids the $O(d^2)$ Fisher matrix storage entirely. However, even 10 CG iterations with double backpropagation is significantly more expensive than PPO's single forward-backward pass, which is the main practical reason PPO replaced TRPO as the default algorithm.
