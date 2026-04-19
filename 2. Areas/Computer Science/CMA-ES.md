**Tags:** #concept #rl
**Related:** [[Evolution Strategies]], [[Evolutionary Computation]], [[Fitness Function]]

## Definition

Covariance Matrix Adaptation Evolution Strategy (CMA-ES) is an advanced evolution strategy for continuous black-box optimisation. It maintains and adapts a full multivariate Gaussian distribution over the search space, effectively learning the local curvature of the fitness landscape.

> [!info] Key Intuition
> CMA-ES is to evolution strategies what second-order methods are to gradient descent: by tracking correlations between parameters, it learns to stretch and rotate its mutation ellipsoid to align with the fitness landscape, making it dramatically more efficient than isotropic ES on ill-conditioned problems.

## How It Works

At each generation, CMA-ES samples $\lambda$ offspring from a multivariate Gaussian:
$$\theta_k \sim \mathcal{N}(\mu, \sigma^2 C), \quad k = 1, \dots, \lambda$$

where:
- $\mu$ is the current mean (best estimate of the optimum)
- $\sigma$ is the overall step size
- $C$ is the covariance matrix encoding directional information

After evaluating fitness, CMA-ES updates:
1. **Mean $\mu$**: shifted toward the weighted centroid of the top-$\mu$ individuals.
2. **Covariance $C$**: updated to capture the directions along which good solutions were found (rank-$\mu$ update + cumulative path length control).
3. **Step size $\sigma$**: adapted via cumulative step-size adaptation (CSA) to maintain a target acceptance rate.

The covariance matrix approximates the **inverse Hessian** of the objective function in the neighbourhood of the current mean, which has been proven for static quadratic models. This makes CMA-ES scale-invariant and rotation-invariant.

> [!example]- CMA-ES on an Ill-Conditioned Function
> For a function with strongly correlated variables like $f(\theta) = \theta_1^2 + 10^6 \theta_2^2$, isotropic ES wastes most mutations. CMA-ES learns that effective search directions are aligned with the axes of the ellipsoid defined by the Hessian and concentrates mutations along $\theta_1$, converging orders of magnitude faster.

> [!warning] Common Misconception
> CMA-ES does **not** use gradient information. The covariance matrix is estimated from fitness rankings only — not from partial derivatives. It is a fully derivative-free method that *approximates* second-order information from population statistics.

## Significance

CMA-ES is considered one of the most powerful general-purpose optimisers for continuous black-box problems of moderate dimensionality (up to ~$10^3$ parameters). It is implemented in Python via the `pymoo` and DEAP libraries. For high-dimensional RL policy optimisation (millions of parameters), OpenAI ES scales better due to its use of a fixed isotropic perturbation.
