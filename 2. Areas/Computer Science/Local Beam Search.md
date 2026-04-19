**Tags:** #concept #rl
**Related:** [[Evolutionary Computation]], [[Genetic Algorithms]]

## Definition

Local Beam Search is a heuristic search algorithm that maintains $W$ states simultaneously rather than one. At each step it generates all successors of all $W$ states and selects the best $W$ from the combined list, concentrating computation on the most promising regions of the search space.

> [!info] Key Intuition
> Local beam search is like $W$ hill climbers that share information: instead of each running independently, they pool their successors and collectively decide which $W$ directions to pursue — abandoning dead ends and concentrating on promising regions.

## How It Works

1. Generate $W$ states randomly.
2. At each step, generate all successors of all $W$ current states.
3. If any successor is a goal state, halt and return it.
4. Otherwise, select the best $W$ successors from the combined list (across all $W$ parent states).
5. Repeat until a goal is found or a stopping condition is met.

### Comparison to Random Restarts

In random-restart hill climbing, $W$ independent searches run in parallel and never communicate. In local beam search, information passes between search threads: useful information discovered by one thread can redirect resources from other threads.

### Stochastic Beam Search

Standard local beam search suffers from diversity loss — all $W$ states may cluster in one region, reducing to a slower form of hill climbing. **Stochastic beam search** selects $W$ successors with probability proportional to fitness (rather than deterministically choosing the top $W$), maintaining diversity.

> [!note] Relationship to Genetic Algorithms
> A genetic algorithm is approximately stochastic beam search with crossover. The analogy: $W$ states correspond to the population; the selection step corresponds to stochastic beam selection; crossover combines genetic material from two states rather than generating successors via local perturbation alone.

> [!warning] Common Misconception
> Local beam search is **not** the same as running $W$ parallel hill climbers. The critical difference is information sharing via the pooled successor list. Without this sharing, it reduces to $W$ independent runs. With sharing, the algorithm can abandon unproductive searches and redirect resources toward productive ones.

## Significance

Local beam search illustrates the population-based principle that underlies evolutionary computation: maintaining diversity while concentrating evaluation on the most promising candidates. Understanding it provides a clean conceptual foundation for genetic algorithms and their relationship to classical search.
