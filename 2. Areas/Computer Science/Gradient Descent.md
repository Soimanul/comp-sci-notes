**Tags:** #concept #algorithm #optimization
**Related:** [[Stochastic Gradient Descent (SGD)]], [[Backpropagation]], [[SLP - Multi-class Classification & Optimization]]

## Definition
A first-order iterative optimization algorithm for finding the local minimum of a differentiable function.

## Mechanism
The parameters $\theta$ are updated by moving in the direction of the negative gradient of the loss function $\mathcal{L}$:
### Gradient Descent (General Form)
**Parameter Update Rule:**
$$
\theta^{(t+1)} = \theta^{(t)} - \eta \, \nabla_{\theta} \mathcal{L}(\theta)
$$

**Notation:**
- $\theta$: parameters (scalar or vector)
- $t$: iteration (step)
- $\eta$: learning rate
- $\mathcal{L}(\theta)$: loss (objective) function
- $\nabla_{\theta} \mathcal{L}(\theta)$: gradient of the loss with respect to $\theta$

### Gradient Descent (ML Form)
**Weight Update Rule:**
$$
\mathbf{w}^{(t+1)} = \mathbf{w}^{(t)} - \eta \, \frac{\partial \mathcal{L}}{\partial \mathbf{w}}
$$

**Notation:**
- $\mathbf{w}$: model weights (parameters)
- $t$: training iteration (step)
- $\eta$: learning rate
- $\mathcal{L}$: loss function (e.g., MSE, cross-entropy)
- $\frac{\partial \mathcal{L}}{\partial \mathbf{w}}$: gradient of the loss w.r.t. the weights, computed via **backpropagation**
## Variants
- **Batch Gradient Descent**: Uses the entire dataset to compute the gradient.
- **[[Stochastic Gradient Descent (SGD)]]**: Uses a single sample or mini-batch.
