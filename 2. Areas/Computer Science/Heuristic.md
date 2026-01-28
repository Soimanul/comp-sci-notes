**Tags:** #concept #cs #algorithms #ai  
**Related:** [[Search Algorithms]], [[Greedy Algorithms]], [[A* Search]], [[Approximation Algorithms]], [[Optimization]]

## Definition
A **heuristic** is a practical rule, strategy, or function used to guide problem-solving toward good solutions **quickly**, typically by using domain insight or simplifying assumptions. Heuristics trade guarantees (optimality, completeness, exactness) for **speed, scalability, or simplicity**.

## Core Idea
Heuristics reduce the search/compute effort by prioritizing what “looks promising,” rather than exhaustively exploring all possibilities.

## Common Forms of Heuristics in CS
1. **Rule-of-thumb procedures (informal heuristics)**
   - Simple decision rules that often work well in practice.
   - _Example:_ “Try the most constrained variable first” in constraint satisfaction problems.

2. **Heuristic functions (numeric guidance)**
   - A function that estimates how close a state is to a goal.
   - _Example (pathfinding):_ `h(n) = ManhattanDistance(n, goal)`.

3. **Greedy selection criteria**
   - Choose the locally best-looking next step.
   - _Example:_ Always pick the next edge with smallest weight (greedy methods).

4. **Pruning / ordering heuristics**
   - Reduce branching by cutting or reordering exploration.
   - _Example:_ Alpha–beta pruning effectiveness depends heavily on good move ordering.

5. **Metaheuristics (higher-level search strategies)**
   - General templates for exploring large spaces when exact optimization is hard.
   - _Examples:_ Simulated annealing, genetic algorithms, tabu search.

## Where Heuristics Show Up
- **Search & Planning:** A*, best-first search, game-playing, CSP solving.
- **Optimization:** NP-hard problems (TSP, scheduling), local search.
- **Systems:** Caching policies, compiler optimizations, network routing, DB query planning.
- **ML/IR:** Feature selection, approximate nearest neighbors, beam search decoding.

## Heuristics vs Algorithms
- An **algorithm** can be heuristic (approximate/empirical) or exact.
- A heuristic typically implies:
  - better average performance or practicality
  - weaker or no guarantees on optimality/correctness in all cases

## Heuristics in A* (Important Special Case)
A* uses a heuristic `h(n)` to estimate remaining cost:
- **Admissible:** never overestimates true remaining cost → A* is optimal (with standard assumptions).
- **Consistent (monotone):** satisfies triangle inequality-like condition → helps efficiency and avoids re-expansions.

## Risks and Failure Modes
- **Bias / blind spots:** heuristic favors a path that looks good but leads to dead ends.
- **Overfitting to typical cases:** works well on common inputs, fails on adversarial ones.
- **Non-optimal results:** may return a “good enough” solution, not the best one.
- **Hidden cost:** computing a heuristic can be expensive; a cheap heuristic may be too weak.

## Rule of Thumb
A useful heuristic is:
- **cheap to compute**
- **strongly correlated with progress toward a goal**
- **safe** when guarantees matter (e.g., admissible in A*)

## Minimal Examples
- **Pathfinding:** use straight-line distance to guide search.
- **Scheduling:** prioritize shortest job first to reduce average waiting time (works in many settings).
- **CSP:** choose the variable with the fewest legal values remaining (MRV heuristic).
