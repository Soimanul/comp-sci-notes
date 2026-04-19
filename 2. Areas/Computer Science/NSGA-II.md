**Tags:** #concept #rl
**Related:** [[Evolutionary Computation]], [[Genetic Algorithms]], [[Selection, Crossover, and Mutation]], [[Fitness Function]]

## Definition

NSGA-II (Non-dominated Sorting Genetic Algorithm II) is a fast, elitist multi-objective genetic algorithm that finds a diverse set of Pareto-optimal solutions by combining non-dominated sorting with crowding distance selection. It was published by Deb, Pratap, Agarwal, and Meyarivan (IEEE Transactions on Evolutionary Computation, 2002).

> [!info] Key Intuition
> When you have two conflicting objectives (e.g. maximise range and minimise acceleration time in an EV), no single solution dominates all others — instead there is a Pareto frontier of optimal trade-offs. NSGA-II evolves an entire population that approximates this frontier.

## How It Works

### Key Concepts

**Pareto Dominance**: Solution $A(x_1, y_1)$ dominates $B(x_2, y_2)$ when:
$$x_1 \leq x_2 \text{ and } y_1 \leq y_2 \text{ and } (x_1 < x_2 \text{ or } y_1 < y_2)$$

**Non-dominated Sorting**: Partition the population into fronts $F_1, F_2, \dots$ where $F_1$ contains all individuals not dominated by any other, $F_2$ all individuals dominated only by those in $F_1$, etc.

**Crowding Distance**: For each individual, the average side length of the cuboid formed by its nearest neighbours in objective space. Boundary solutions receive $\infty$.
$$d(i) = d(i) + \frac{o(i+1) - o(i-1)}{o(\max) - o(\min)}$$
summed over all objectives $o$.

### Main Loop

1. Combine parent population $P_t$ and offspring $Q_t$ into combined population $R_t = P_t \cup Q_t$.
2. Apply **non-dominated sorting** to produce fronts $F_1, F_2, \dots$
3. Fill the new population $P_{t+1}$ front by front. When a front cannot fit entirely, sort individuals within it by crowding distance (descending) and take the most spread-out members.

### Offspring Production (within each generation)

1. **Binary tournament selection**: compare two randomly drawn individuals; the one with better rank wins; if ranks are equal, the one with larger crowding distance wins (less crowded = more diverse).
2. **Crossover** (recombine selected parents).
3. **Mutation** (perturb offspring).

> [!example]- EV Design Optimisation
> Objectives: minimise 0–100 km/h acceleration time; maximise range.
> Variables: tyre size, motor power, battery capacity.
> NSGA-II evolves a population whose final non-dominated front approximates the full Pareto curve — giving designers the complete trade-off space rather than a single "best" solution.

> [!warning] Common Misconception
> NSGA-II does **not** find a single optimal solution. It finds a set of Pareto-optimal solutions, and the choice between them is a human (engineering/policy) decision. Using a scalarised weighted objective instead defeats the purpose of multi-objective optimisation.

## Significance

NSGA-II is the standard benchmark algorithm for multi-objective evolutionary optimisation. It is available in Python via `pymoo` and DEAP. Its two-level comparison operator (rank first, then crowding distance) elegantly balances convergence toward the Pareto front with diversity along it.
