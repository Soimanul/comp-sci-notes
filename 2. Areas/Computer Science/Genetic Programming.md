**Tags:** #concept #rl
**Related:** [[Evolutionary Computation]], [[Genetic Algorithms]], [[NEAT]]

## Definition

Genetic Programming (GP) is a subfield of genetic algorithms in which the individuals being evolved are programs rather than fixed-length bit strings. Programs are represented as syntax trees (parse trees), and the crossover operator splices subtrees to produce syntactically valid offspring.

> [!info] Key Intuition
> Where a GA evolves a fixed-length parameter vector, GP evolves the program structure itself — it is the evolutionary analogue of AutoML/neural architecture search applied to arbitrary code.

## How It Works

Each individual in the population is a syntax tree. The nodes of the tree are functions (operators such as `+`, `sin`, `if`), and the leaves are terminals (constants or input variables).

**Crossover** in GP involves:
1. Randomly selecting a subtree node in each parent.
2. Swapping the subtrees to produce two offspring.
3. Offspring are guaranteed to be syntactically well-formed (closed under the operator set).

**Mutation** applies random perturbations such as replacing a subtree with a newly generated random subtree.

**Representations used in practice:**
- LISP s-expressions (original Koza 1992 formulation)
- Standard language parse trees (C, Python)
- Specially designed formats for electronic circuits, robot controllers, neural architectures

### Applications in ML/RL

GP currently presents a broad range of opportunities in numerical-algorithm paradigms:
- **NEAT**: evolves neural network topologies as augmenting tree/graph structures
- **FREVO**: framework for evolving arbitrary agent representations (ANNs, FSMs, fuzzy rules) for RL tasks
- **Neural Architecture Search (NAS)**: regularised evolution for image classifier architecture search (Real et al., Google Brain)

> [!example]- Evolving a Controller Program
> Target: a robot controller that steers toward a light source. The GP population consists of programs over sensor inputs (light intensity, angle). After evolution, a tree like `(if (> light_left light_right) turn_left turn_right)` may emerge — a human-readable interpretable controller.

> [!warning] Common Misconception
> GP programs are **not** arbitrary code — operators must form a closed set (any function node can take any terminal or function node as its argument). Without this closure property, crossover produces syntactically invalid offspring.

## Significance

Genetic programming extends the reach of evolutionary search from parameter vectors to the space of programs and architectures. In the RL context, it enables the joint optimisation of both the policy representation and its parameters, as exemplified by NEAT and modern neural architecture search.
