**Tags:** #concept #rl
**Related:** [[Q-Learning]], [[Markov Decision Process]], [[Action-Value Estimation]], [[Practice Review]]

## Definition

State Discretization is the process of mapping a continuous state space into a finite set of discrete bins so that tabular RL methods (e.g. Q-tables) can be applied to environments with real-valued observations.

> [!info] Key Intuition
> A Q-table needs a finite number of rows — one per state. Continuous states have infinitely many values, so you round each dimension into buckets (like rounding temperature to the nearest 5°C) to create a manageable table.

## How It Works

Given a continuous state vector $s = (x_1, x_2, \ldots, x_n)$, each dimension is divided into $k_i$ equal-width (or equal-frequency) bins:

1. Define bounds $[\text{low}_i, \text{high}_i]$ for each dimension
2. Create $k_i$ bins: $\text{bin}(x_i) = \lfloor (x_i - \text{low}_i) / (\text{high}_i - \text{low}_i) \cdot k_i \rfloor$
3. Represent the state as the tuple of bin indices: $\hat{s} = (\text{bin}(x_1), \ldots, \text{bin}(x_n))$
4. Use $\hat{s}$ as the Q-table key

The total number of table entries is $\prod_i k_i$, which grows exponentially with the number of dimensions (**curse of dimensionality**).

### Acrobot-v1 Example

Acrobot has a 6-dimensional continuous state (joint angles and angular velocities). Using 10 bins per dimension yields $10^6 = 1{,}000{,}000$ states — a large but manageable table. The bin resolution determines the trade-off between approximation error (too coarse) and table size/sparsity (too fine).

> [!example]- Bin Construction
> State dimension $x_1 \in [-\pi, \pi]$, using 10 bins:
> Bin width = $2\pi / 10 \approx 0.628$
> $x_1 = 1.2 \Rightarrow \text{bin} = \lfloor (1.2 + \pi) / 0.628 \rfloor = \lfloor 6.9 \rfloor = 6$
> The agent maps state $x_1 = 1.2$ to bucket 6 for Q-table lookup.

> [!warning] Common Misconception
> Finer bins do not always improve performance. Very fine discretisation leads to a sparse Q-table where most states are never visited, meaning Q-values remain at their initialisation and the agent cannot generalise. Coarser bins introduce approximation error but allow faster learning. Function approximation (e.g. DQN) avoids this trade-off entirely by generalising continuously.

## Significance

State Discretization is the standard bridge between continuous environments and tabular RL, and is particularly relevant for comparing Q-table performance against neural-network-based methods. It illustrates why deep RL methods like DQN or PPO are preferred for high-dimensional or truly continuous state spaces.
