**Tags:** #concept #rl
**Related:** [[Evolutionary Computation]], [[Genetic Algorithms]], [[Selection, Crossover, and Mutation]]

## Definition

A fitness function is a function that takes a candidate solution (chromosome) as input and produces a scalar score representing how well that solution solves the problem at hand. It is the sole interface between the evolutionary algorithm and the problem domain.

> [!info] Key Intuition
> The fitness function is the evolutionary analogue of the loss function in gradient-based learning — it defines what "good" means, but unlike a loss function it need not be differentiable.

## How It Works

At each generation, every individual in the population is decoded from its genotype representation and evaluated by the fitness function. The resulting scalar guides selection: individuals with higher fitness are more likely to reproduce.

The fitness function may coincide with the problem's objective function, or it may be a modified version designed for numerical reasons (e.g. shifted so all values are positive for roulette-wheel selection).

In RL applications the fitness of a neural-network controller is typically the total episode reward accumulated by running the agent for a full episode.

**Incremental fitness shaping** is an extension where the fitness function is defined as a state machine over behavioural milestones. Rather than measuring raw task performance, it grants bonuses when the agent satisfies ordered sub-goals, effectively embedding curriculum structure into the evolutionary signal.

> [!example]- Knapsack Problem Fitness
> Given items with weights $w_i$ and profits $p_i$ and a knapsack capacity $C$, a chromosome $x \in \{0,1\}^n$ encodes which items to include. The fitness is:
> $$f(x) = \sum_{i} x_i \cdot p_i \quad \text{subject to} \quad \sum_i x_i \cdot w_i \leq C$$
> If the weight constraint is violated, the chromosome is penalised (fitness = 0 or heavily discounted).

> [!warning] Common Misconception
> The fitness function is **not** the same as the objective function in general. The objective function describes what you want to optimise; the fitness function is the computable proxy used by the algorithm. They coincide only when the objective is directly measurable and well-scaled.

## Significance

Fitness function design is often the most consequential engineering decision in applying evolutionary computation. A poorly designed fitness function leads to deceptive landscapes where the algorithm converges to local optima far from the true solution. In RL, fitness shaping analogises to reward shaping and faces the same potential pitfalls.
