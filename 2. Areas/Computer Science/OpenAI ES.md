**Tags:** #concept #rl
**Related:** [[Evolution Strategies]], [[Neuroevolution]], [[Evolutionary Computation]], [[Reinforcement Learning]]

## Definition

OpenAI ES (Evolution Strategies as a Scalable Alternative to Reinforcement Learning, Salimans et al. 2017) is a distributed, parallelised evolution strategy for optimising deep neural network policies. It treats the policy parameters as the genome and episode return as the fitness, using an isotropic Gaussian perturbation scheme that is communication-efficient and highly scalable.

> [!info] Key Intuition
> OpenAI ES is essentially a parallelised finite-difference gradient estimator: each worker applies a different random perturbation to the shared policy, evaluates it, and reports a scalar; the workers then combine their scalars to reconstruct a pseudo-gradient update — without ever backpropagating through the environment.

## How It Works

### Algorithm

At iteration $t$ with policy parameters $\theta_t$ and perturbation scale $\sigma$:

1. Sample $n$ noise vectors $\epsilon_1, \dots, \epsilon_n \sim \mathcal{N}(0, I)$ (one per worker).
2. Each worker $i$ evaluates the perturbed policy $\theta_t + \sigma \epsilon_i$ in the environment and reports fitness $F_i$.
3. Compute the parameter update:
$$\theta_{t+1} = \theta_t + \frac{\alpha}{n\sigma} \sum_{i=1}^{n} F_i \epsilon_i$$

This is equivalent to a stochastic estimate of $\nabla_\theta \mathbb{E}[F(\theta)]$ via the log-derivative trick.

### Scalability

Because workers only communicate scalar fitness values $F_i$ (not gradients), communication overhead is minimal. With $n = 1440$ workers, a 3D MuJoCo locomotion task that takes 10 hours with A3C converges in under 10 minutes.

### Mirrored Sampling (Antithetic Noise)

To reduce variance, each perturbation $\epsilon_i$ is paired with $-\epsilon_i$, so the fitness estimates cancel out the component of variance due to the noise direction.

> [!example]- MuJoCo Humanoid
> OpenAI ES trained a humanoid walking policy with 4 million parameters using 1440 CPU workers. It achieved comparable reward to A3C and TRPO in wall-clock time, demonstrating that population-based derivative-free methods can scale to deep RL.

> [!warning] Common Misconception
> OpenAI ES is **not** a standard genetic algorithm. It uses no crossover, no selection of survivors from a population — it is a single-point ES variant that maintains one mean policy and perturbs it with isotropic noise. The "population" is recreated from scratch each generation using a shared random seed.

## Significance

OpenAI ES demonstrated in 2017 that carefully engineered ES methods can match deep RL algorithms on continuous control benchmarks while offering superior parallelism, simpler implementation, and robustness to reward sparsity and long time horizons. It renewed interest in derivative-free optimisation for deep RL.
