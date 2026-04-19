**Tags:** #topic #hub #rl
**Related:** [[Reinforcement Learning]], [[Introduction to Reinforcement Learning]]

## Overview

Evolutionary computation is a family of population-based, metaheuristic optimization algorithms inspired by biological evolution. Rather than computing gradients, these methods iteratively select, recombine, and mutate a population of candidate solutions, driving the population toward higher fitness over successive generations. This hub covers the core paradigms — Genetic Algorithms, Evolution Strategies, and Neuroevolution — as well as multi-objective extensions and the application of these ideas to RL and neural architecture search.

> [!abstract]- TL;DR
> Evolutionary computation solves optimization problems by maintaining a population of solutions, scoring each by a fitness function, and breeding better solutions through selection, crossover, and mutation. It is derivative-free, highly parallelizable, and naturally suited to problems where gradient information is unavailable or the search space is discrete.

## Knowledge Map

### 1. Foundations
- [[Fitness Function]]
- [[Genetic Algorithms]]
- [[Selection, Crossover, and Mutation]]

### 2. Advanced Variants
- [[Evolution Strategies]]
- [[CMA-ES]]
- [[Genetic Programming]]

### 3. Multi-Objective Optimization
- [[NSGA-II]]

### 4. Neuroevolution
- [[Neuroevolution]]
- [[NEAT]]

### 5. Modern Evolutionary Methods for RL
- [[OpenAI ES]]
- [[Population-Based Training]]
- [[Local Beam Search]]

> [!question]- Common Exam Questions
> - What is the role of the fitness function in a genetic algorithm, and how does it differ from an objective function?
> - Describe the three main genetic operators (selection, crossover, mutation) and give one concrete variant of each.
> - How does NSGA-II handle multi-objective optimization, and what is the purpose of crowding distance?
> - What are the three key innovations in NEAT that distinguish it from earlier neuroevolution approaches?
