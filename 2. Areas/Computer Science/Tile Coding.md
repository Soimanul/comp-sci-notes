**Tags:** #concept #rl
**Related:** [[Approximation Methods]], [[Linear Function Approximation]], [[Radial Basis Functions]], [[Value Function Approximation]]

## Definition

Tile coding is a form of coarse coding for multi-dimensional continuous state spaces. The state space is partitioned into overlapping grids, each called a **tiling**; each cell within a tiling is called a **tile**. A state $s$ activates exactly one tile per tiling, producing a sparse binary feature vector.

> [!info] Key Intuition
> Multiple offset tilings work together — no single tiling has fine resolution, but *where* tilings overlap reveals fine-grained distinctions. A state's representation is the intersection of its tiles across all tilings.

## How It Works

Given $n$ tilings of a $k$-dimensional state space:

1. Each tiling partitions the space into a rectangular grid, offset slightly from the others.
2. For a query state $s$, identify which tile it falls into in each tiling.
3. Set those $n$ features to 1; all other features are 0.
4. The resulting binary feature vector $\mathbf{x}(s)$ has exactly $n$ ones among $n \times |\text{tiles per tiling}|$ entries.

The linear value estimate is then $\hat{v}(s, \mathbf{w}) = \mathbf{w}^\top \mathbf{x}(s)$, which simply sums the weights for the $n$ active tiles.

Because only $n$ weights are ever non-zero, the gradient update costs $O(n)$ — independent of the total number of tiles.

> [!example]- 2D State Space with 4 Tilings
> For a 2D continuous space (e.g. position × velocity in MountainCar), use 4 tilings, each shifted by a fraction of a tile width. A point $(p, v)$ activates one tile in each of the 4 tilings. Two nearby points share more active tiles than distant points — the number of shared tiles serves as a similarity measure.

> [!warning] Common Misconception
> Tile coding does not require storing a feature vector explicitly. Only the indices of the $n$ active tiles need be computed (typically via hashing). This makes tile coding extremely memory-efficient even for large state spaces.

## Significance

Tile coding may be the most practical feature representation for continuous-space RL on sequential digital computers. It is computationally efficient (binary features, sparse gradient), flexible (tile width and number control resolution vs. generalisation), and has been used in classic RL benchmarks like Mountain Car and Acrobot.
