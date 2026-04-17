**Tags:** #concept #rl
**Related:** [[Markov Assumption]], [[Markov Decision Process]], [[Graphs, Search, and MDPs]]

## Definition

A stochastic process $\{X_n\}_{n \geq 0}$ over a state space $\mathcal{S}$ satisfying the **Markov property**: the probability of the next state depends only on the current state, not on the history of past states.

$$\mathbb{P}(X_{n+1} = s' \mid X_n, X_{n-1}, \ldots, X_0) = \mathbb{P}(X_{n+1} = s' \mid X_n)$$

> [!info] Key Intuition
> The current state is a sufficient statistic for the future — the history adds no information beyond what the present state already encodes.

## Transition Matrix

For a finite Markov chain over $|\mathcal{S}|$ states, the dynamics are fully described by a **stochastic transition matrix** $P$ where $P_{ij} = \mathbb{P}(X_{n+1} = j \mid X_n = i)$. Each row sums to 1.

Matrices and graphs are dual: $P_{ij}$ is also the weighted adjacency matrix of a directed graph over states.

## Stationary Distribution

A distribution $\mu$ is stationary if $\mu P = \mu$. For an **irreducible** (all states reachable from all others) finite Markov chain, a unique stationary distribution exists (**Perron-Frobenius theorem**).

## Absorbing Markov Chains

A state $s$ is **absorbing** if $P_{ss} = 1$ (once entered, never left). Absorbing chains unify episodic and continuing RL tasks: terminal states become absorbing states with zero reward, and the episode length corresponds to absorption time.

The **fundamental matrix** $N = (I - Q)^{-1}$ gives expected visitation counts for transient states before absorption.

> [!example]- Worked Example
> A 2-state chain: state A transitions to B with prob 0.3, stays in A with 0.7. State B is absorbing. The expected number of steps before absorption from A = $N_{AA} = (1-0.7)^{-1} = 3.33$.

> [!warning] Common Misconception
> The Markov property is a restriction on **state representation**, not on the decision process. An agent can have memory or use a complex policy — as long as the chosen state encodes all relevant history, the process is Markov.

## Significance

Markov chains are the mathematical substrate of MDPs. Understanding chain structure (irreducibility, absorption, stationary distribution) explains convergence properties of RL algorithms.
