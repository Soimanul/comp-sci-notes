**Tags:** #concept #rl
**Related:** [[Evolutionary Computation]], [[Fitness Function]], [[Selection, Crossover, and Mutation]], [[Genetic Programming]], [[NEAT]]

## Definition

A Genetic Algorithm (GA) is a search-based optimisation technique inspired by Darwinian evolution. It maintains a population of candidate solutions encoded as chromosomes, iteratively applying selection, crossover, and mutation to produce fitter generations until a termination criterion is met.

> [!info] Key Intuition
> A GA is approximately stochastic beam search with crossover: it keeps $k$ promising states in parallel, but instead of just mutating them it recombines pairs to produce offspring that inherit traits from both parents.

## How It Works

### Terminology

| Term | Meaning |
|---|---|
| **Population** | Set of all current candidate solutions (chromosomes) |
| **Chromosome** | One encoded candidate solution |
| **Gene** | One element position of a chromosome |
| **Allele** | The value a gene takes for a particular chromosome |
| **Genotype** | Population in the computation space (encoded representation) |
| **Phenotype** | Population in the real-world solution space (decoded representation) |

### Chromosome Representations

- **Binary**: bit string, e.g. `[0 0 1 0 1 1 1 0 0 1]`
- **Real-valued**: floating-point vector, e.g. `[0.5 0.2 0.6 ...]`
- **Integer**: integer vector
- **Permutation**: ordering of indices (used for routing/scheduling)

### Main Loop

```
function GENETIC-ALGORITHM(population, fitness):
  repeat
    weights ← WEIGHTED-BY(population, fitness)
    for i = 1 to SIZE(population):
      parent1, parent2 ← WEIGHTED-RANDOM-CHOICES(population, weights, 2)
      child ← REPRODUCE(parent1, parent2)
      if (small random probability): child ← MUTATE(child)
      add child to population2
    population ← population2
  until termination criterion
  return best individual according to fitness
```

### Termination Conditions

- No improvement in the population for $X$ iterations
- Absolute number of generations reached
- Objective function value exceeds a threshold

### Key Parameters

- Population size
- Number of generations
- Percentage of elite selection (elitism)
- Mutation rate
- Crossover rate

### Advantages and Limitations

**Advantages:** derivative-free; handles discrete and continuous spaces; highly parallelisable; provides a set of good solutions rather than a single one.

**Limitations:** computationally expensive per generation (fitness must be evaluated for every individual); no optimality guarantees; can fail to converge if poorly configured.

> [!example]- Knapsack Problem with GA
> Encode each item as a bit in a binary chromosome. Fitness = total profit if total weight ≤ capacity, else 0. Run selection → crossover → mutation for $N$ generations. The chromosome with highest fitness in the final generation is the approximate solution.

> [!warning] Common Misconception
> GAs are **not** biologically accurate simulations of evolution. The mathematical operators (crossover, mutation, selection) are loosely inspired by biological processes but are in no way exact replicas — they are optimisation heuristics. Do not conflate them with population genetics.

## Significance

GAs are the most widely used family within evolutionary computation (dominant in publication count since 2008). They are particularly well suited to combinatorial optimisation problems (e.g. scheduling, routing, hyperparameter search) and to RL problems where gradient information is unavailable.
