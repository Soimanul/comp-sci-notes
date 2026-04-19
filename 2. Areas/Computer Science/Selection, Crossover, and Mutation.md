**Tags:** #concept #rl
**Related:** [[Evolutionary Computation]], [[Genetic Algorithms]], [[Fitness Function]]

## Definition

Selection, crossover, and mutation are the three fundamental genetic operators in evolutionary algorithms. Selection chooses which individuals reproduce; crossover combines genetic material from two parents; mutation introduces random perturbations into offspring.

> [!info] Key Intuition
> Selection exploits current good solutions; crossover recombines them to explore new combinations; mutation ensures diversity and prevents premature convergence to local optima. All three must be balanced.

## Selection

Chromosomes are chosen as parents for crossover based on their fitness. Several schemes exist:

**Roulette Wheel (Fitness Proportionate Selection, FPS)**
Each chromosome is allocated a section of a wheel proportional to its fitness. A random spin selects a parent. High-fitness individuals have larger sections.

Algorithm:
1. Compute sum $S$ of all fitnesses.
2. Draw $r \sim \text{Uniform}(0, S)$.
3. Walk through population accumulating fitness until the cumulative sum exceeds $r$; return that chromosome.

**Stochastic Universal Sampling (SUS)**
An extension of FPS with a single random offset and evenly spaced pointers, giving weaker members a fairer chance and reducing spread.

**Tournament Selection**
Randomly pick $k$ chromosomes; the one with highest fitness wins and becomes a parent. Used in NSGA-II with $k=2$.

**Rank Selection**
Re-rank chromosomes 1…$N$ by fitness and assign selection probability by rank rather than raw fitness. Prevents one dominant individual from monopolising selection.

**Elitism**
Copy the best $e$ chromosomes directly to the next generation before crossover/mutation. Prevents losing the best solution found so far.

**Survivor Selection**
After producing offspring, choose which individuals persist:
- **Age-based**: oldest chromosomes are replaced.
- **Fitness-based**: lowest-fitness chromosomes are replaced.

## Crossover

Two parents produce offspring by combining their genetic material:

**One-Point Crossover**
Choose a random split point $c$; child inherits genes $1 \dots c$ from parent 1 and genes $c+1 \dots n$ from parent 2.

**Multi-Point Crossover**
Multiple split points; segments alternate between parents.

**Uniform Crossover**
Each gene is independently inherited from either parent with probability 0.5.

## Mutation

Mutation introduces small random changes to maintain population diversity:

| Operator | Description |
|---|---|
| **Bit Flip** | Flip a randomly selected bit (binary chromosomes) |
| **Random Resetting** | Replace a gene with a random value from its domain |
| **Swap Mutation** | Swap two randomly selected genes |
| **Scramble Mutation** | Randomly shuffle a random subsequence |
| **Inversion Mutation** | Reverse a random subsequence |

Mutation probability is kept small (e.g. 1–5%) to avoid destroying fit structures.

> [!example]- One-Point Crossover
> Parent 1: `[0 1 2 3 4 | 5 6 7 8 9]`
> Parent 2: `[5 8 9 4 2 | 3 5 7 5 8]`
> Split at position 4 →
> Child 1: `[0 1 2 3 4 3 5 7 5 8]`
> Child 2: `[5 8 9 4 2 5 6 7 8 9]`

> [!warning] Common Misconception
> High mutation rates do **not** improve search — they degrade it. With very high mutation, the GA degenerates into random search. Mutation is a diversity maintenance operator, not a primary search mechanism.

## Significance

The choice and tuning of these operators determines convergence speed and solution quality. Tournament selection is preferred in multi-objective settings (NSGA-II) because it works on relative fitness rankings, which remain meaningful across objectives.
