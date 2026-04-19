**Tags:** #concept #rl
**Related:** [[Evolutionary Computation]], [[NEAT]], [[Genetic Algorithms]], [[Genetic Programming]], [[Reinforcement Learning]]

## Definition

Neuroevolution is the application of evolutionary algorithms to the optimisation of artificial neural networks. It can evolve network weights, architecture (topology), or both simultaneously, without requiring gradient information.

> [!info] Key Intuition
> Where backpropagation climbs the gradient of a loss function, neuroevolution applies survival-of-the-fittest to a population of neural networks — each network is evaluated as a whole by running it in the environment, and only the fittest networks reproduce.

## How It Works

### Historical Progression

- **Pre-NEAT (before 2001)**: research focused on evolving weights only; the network topology was fixed before evolution began.
- **NEAT (2001)**: shifted focus to co-evolving both weights and topology, enabling the discovery of minimal effective architectures.

NEAT specifically explores weight space via crossover of network weights and mutation of a single network's weights — framing evolution as an alternative to backpropagation for optimising neural network policies.

### Motivations for Neuroevolution

Neuroevolution is most useful when:
- **Reinforcement Learning**: sparse or delayed rewards make gradient estimation difficult.
- **Control tasks**: tuning PID controllers or other feedback systems.
- **AutoML**: automated discovery of machine learning pipelines.
- **HPO (Hyperparameter Optimisation)**: treating hyperparameters as genes.
- **Neural Architecture Search (NAS)**: evolving entire network designs (e.g. AmoebaNet — regularised evolution for image classifiers, Real et al., Google Brain).

### FREVO Framework

FREVO (Framework for Evolutionary Optimisation) applies neuroevolution to RL agents:
1. Maintain a pool of candidate network representations (ANNs, FSMs, fuzzy rules).
2. For each generation: evaluate agents in the problem environment, rank by fitness, select, mutate and combine.
3. The agent representation is optimised to maximise fitness on the given task.

Applied example: evolving recurrent neural network controllers for the Lunar Lander environment using incremental fitness shaping (University of Sussex, 2019).

> [!example]- Neuroevolution vs Q-Learning
> In the PyRace car-driving environment, a Q-table approach struggles with continuous state space (requiring discretisation). A neuroevolution approach (NEAT) evolves networks with 5 distance-sensor inputs directly, discovering effective driving policies in tens of generations without ever computing a gradient.

> [!warning] Common Misconception
> Neuroevolution is **not** a subset of reinforcement learning. It is an alternative optimisation paradigm. The fitness function plays the role of a reward signal, but there is no Bellman equation, no value function, and no credit assignment through time — fitness is evaluated episodically at the population level.

## Significance

Neuroevolution provides a practical alternative to gradient-based RL when: (1) the environment is non-differentiable, (2) rewards are extremely sparse, or (3) the right network architecture is unknown. Its main limitation is that evaluating fitness requires running full episodes for every individual in every generation, making it computationally expensive. Modern variants like [[OpenAI ES]] address this by parallelising across thousands of workers.
