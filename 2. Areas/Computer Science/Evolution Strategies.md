**Tags:** #concept #rl
**Related:** [[Evolutionary Computation]], [[CMA-ES]], [[Genetic Algorithms]], [[Fitness Function]]

## Definition

Evolution Strategies (ES) are a class of derivative-free, population-based optimisation algorithms that operate on real-valued parameter vectors. They rely primarily on mutation (adding Gaussian noise) and deterministic selection based on fitness rankings rather than fitness values.

> [!info] Key Intuition
> ES replaces gradient descent with perturbation: instead of computing $\nabla_\theta J$, it estimates a search direction by sampling noisy variants of the current parameters and averaging the perturbations weighted by their fitness rankings.

## How It Works

### Mutation

For real-valued search spaces, mutation is performed by adding a normally distributed random vector:
$$\theta' = \theta + \sigma \cdot \epsilon, \quad \epsilon \sim \mathcal{N}(0, I)$$

The step size $\sigma$ (standard deviation) governs mutation strength and can be adapted via **self-adaptation** (an evolving strategy parameter) or via covariance matrix adaptation ([[CMA-ES]]).

### Selection

ES selection is **deterministic and rank-based**: only the top-$\mu$ individuals by fitness rank survive, regardless of the magnitude of their fitness values. This makes ES **invariant under monotonic transformations of the objective function** — a highly desirable robustness property.

### ES Variants

| Notation | Description |
|---|---|
| $(1+1)$-ES | One parent, one mutant; keep the better one |
| $(1,\lambda)$-ES | One parent, $\lambda$ mutants; best mutant becomes the next parent; current parent always discarded |
| $(\mu/\rho+, \lambda)$-ES | $\mu$ parents, recombination, $\lambda$ offspring; reduces susceptibility to local optima |

### Historical Note

ES was created in the early 1960s and developed in the 1970s by Ingo Rechenberg and Hans-Paul Schwefel. The covariance matrix adaptation variant ([[CMA-ES]]) is the most powerful modern descendant.

> [!example]- (1+1)-ES
> Start with parameter vector $\theta_0$. At each step:
> 1. Sample $\theta' = \theta + \sigma \epsilon$, $\epsilon \sim \mathcal{N}(0,I)$.
> 2. If $f(\theta') \geq f(\theta)$, set $\theta \leftarrow \theta'$.
> 3. Adapt $\sigma$ via the 1/5-success rule: if more than 1 in 5 mutations improve fitness, increase $\sigma$; otherwise decrease it.

> [!warning] Common Misconception
> ES is **not** the same as random hill climbing. ES uses adaptive step sizes, rank-based selection, and (in advanced variants) a full covariance model of the search landscape — making it substantially more powerful than naive random perturbation.

## Significance

ES methods are the foundation of modern black-box optimisation for RL. The OpenAI ES (2017) scales the $(1,\lambda)$-ES idea to thousands of parallel workers and achieves competitive performance with deep RL on continuous control benchmarks, demonstrating that gradient-free optimisation can match gradient-based methods at scale.
