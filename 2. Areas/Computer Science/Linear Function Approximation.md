**Tags:** #concept #rl
**Related:** [[Approximation Methods]], [[Value Function Approximation]], [[Tile Coding]], [[Radial Basis Functions]], [[Semi-Gradient TD]]

## Definition

Linear Function Approximation represents the value function as a linear combination of state features:

$$\hat{v}(s, \mathbf{w}) \doteq \mathbf{w}^\top \mathbf{x}(s) \doteq \sum_{i=1}^{d} w_i x_i(s)$$

where $\mathbf{x}(s) = (x_1(s), \ldots, x_d(s))^\top$ is the **feature vector** of state $s$ and $\mathbf{w}$ is the weight vector.

> [!info] Key Intuition
> Linear approximation is the most theoretically well-understood case: with semi-gradient TD it converges to a unique fixed point near the true value function, and its gradient is simply the feature vector $\nabla\hat{v}(s,\mathbf{w}) = \mathbf{x}(s)$.

## SGD Update for Linear VFA

Because $\nabla\hat{v}(s, \mathbf{w}) = \mathbf{x}(s)$, the semi-gradient TD(0) update simplifies to:

$$\mathbf{w}_{t+1} \leftarrow \mathbf{w}_t + \alpha\left[R_{t+1} + \gamma\hat{v}(S_{t+1}, \mathbf{w}_t) - \hat{v}(S_t, \mathbf{w}_t)\right]\mathbf{x}(S_t)$$

Linear TD is guaranteed to converge (in the on-policy case) to the **TD fixed point** $\mathbf{w}_{TD}$, where $\overline{VE}(\mathbf{w}_{TD}) \leq \frac{1}{1-\gamma}\min_{\mathbf{w}} \overline{VE}(\mathbf{w})$.

## Feature Construction Methods

The choice of feature representation determines what the linear model can express:

| Method | Description |
|--------|-------------|
| **Polynomials** | Simple but generalise poorly in online RL settings |
| **Fourier basis** | Weighted sums of sine/cosine functions; often better than polynomials |
| **Coarse coding** | Binary features based on overlapping receptive fields (circles in state space) |
| **Tile coding** | Practical form of coarse coding using overlapping grids; see [[Tile Coding]] |
| **Radial basis functions** | Generalise coarse coding to soft, continuous activations; see [[Radial Basis Functions]] |

> [!example]- Tabular as a Special Case
> A tabular value function is a special case of linear approximation where $\mathbf{x}(s)$ is a one-hot vector — a 1 in position $s$ and 0 elsewhere. Each weight $w_s$ then corresponds exactly to $V(s)$. This shows linear methods are strictly more general than tabular methods.

> [!warning] Common Misconception
> Linear semi-gradient TD converges to the TD fixed point, *not* to the minimum of $\overline{VE}$. The TD fixed point is always within a bounded factor of the true optimum, but it is not the same thing — nonlinear methods (ANNs) can represent the optimum but may not converge at all under bootstrapping.

## Significance

Linear function approximation is the theoretically safest regime for approximation in RL: convergence results are strongest here, and the LSTD algorithm can find the TD fixed point with data-efficiency proportional to $d^2$ (quadratic). All tabular and state-aggregation methods are special cases.
