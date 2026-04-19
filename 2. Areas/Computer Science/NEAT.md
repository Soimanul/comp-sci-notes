**Tags:** #concept #rl
**Related:** [[Reinforcement Learning]], [[Evolutionary Computation]], [[Neuroevolution]], [[Genetic Programming]], [[Exploration-Exploitation Tradeoff]], [[Curriculum Learning]]

## Definition

NEAT (NeuroEvolution of Augmenting Topologies) is a genetic algorithm that evolves both the weights and the topology of neural networks simultaneously, using speciation to protect innovation and prevent premature convergence.

> [!info] Key Intuition
> NEAT treats the neural network architecture itself as a genome — not just the weights — so evolution can discover the right network structure for a task rather than requiring it to be hand-designed.

## How It Works

NEAT maintains a population of agents (genomes), each encoding a neural network. Each generation:

1. **Evaluate** all agents using a fitness function (e.g. distance driven before crashing)
2. **Select** the fittest individuals to reproduce
3. **Crossover** high-fitness genomes
4. **Mutate** — randomly add nodes, add connections, or perturb weights
5. **Speciate** — group similar genomes so structural innovations are not immediately eliminated by competition with more evolved structures

In the IE PyRace context: each car is an agent; when all cars crash, a fitness score is assigned based on track distance covered; the next generation is bred from the survivors.

> [!example]- PyRace NEAT Setup
> Population of cars, each driven by a neural network with 5 sensor inputs (short-range distance sensors: front-left, left, front, right, front-right) and action outputs (steer/accelerate). Generation 1 starts with random topologies; over generations, survivors are those that navigate further along the track without collision.

> [!warning] Common Misconception
> NEAT is **not** reinforcement learning in the strict TD/policy-gradient sense — there is no reward signal propagated backwards through time. Fitness is evaluated episodically at the end of each generation, not incrementally per step. The two approaches (NEAT vs Q-Table) are compared directly in the PyRace environment.

## Significance

NEAT excels at tasks where the right architecture is unknown and training data is sparse. For car driving with few sensors and a continuous-space problem where tabular Q-Learning struggles with state discretisation, NEAT often converges faster to a working policy. Its main drawback is that fitness evaluation requires running entire episodes for every individual in every generation, making it computationally expensive at scale.

## From Evolutionary Computation

The lecture formalises the three key innovations that distinguish NEAT from earlier neuroevolution:

1. **Historical Marking Crossover (Gene Alignment)**: Each connection gene carries an **innovation number** assigned globally when it first appears. When two genomes with different topologies cross over, genes with matching innovation numbers are aligned; disjoint and excess genes are inherited from the fitter parent. This solves the **competing conventions problem** — where two structurally equivalent networks encode the same node with different indices, making naive crossover produce non-functional offspring.

2. **Speciation**: Genomes are grouped into species based on a compatibility distance measure (number of excess/disjoint genes + weight differences). Fitness is **shared** within species (explicit fitness sharing): each individual's fitness is divided by the number of members in its species. This protects topological innovations that need several generations to optimise from being immediately eliminated by more evolved but structurally simpler competitors.

3. **Complexifying (Minimal Structure Initialisation)**: All networks start with a minimal topology (no hidden nodes, only input→output connections). Complexity grows only as mutations add nodes and connections — avoiding the need to specify a topology before evolution begins.

### NEAT Encoding

Each genome contains two lists:
- **Node genes**: list of node IDs with types (sensor, hidden, output).
- **Connection genes**: each connection encodes `(in_node, out_node, weight, enabled, innovation_number)`. A connection can be disabled (marked DISABLED) without being deleted, allowing it to re-enable in future generations.

### Mutations

- **Add connection**: a new connection between two previously unconnected nodes; receives a new innovation number.
- **Add node**: an existing connection is disabled and replaced by two new connections via a new hidden node; receives new innovation numbers.
- **Perturb weights**: Gaussian noise added to connection weights.

### Python Implementation

The NEAT-Python library (pure Python, no dependencies beyond stdlib) implements the full NEAT algorithm with configurable activation functions, genome interface, and reproduction interface. Documentation: https://neat-python.readthedocs.io/en/latest/
