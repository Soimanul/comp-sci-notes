**Tags:** #concept #neural-networks
**Related:** [[Activation Functions]], [[Layer Vector Computation]], [[Feedforward Neural Network]]

## Definition
A single neuron is a parametric nonlinear function that maps an input vector $x \in \mathbb{R}^n$ to a scalar output:
$$y = \sigma\!\left(w^\top x + b\right)$$
where $w \in \mathbb{R}^n$ is the weight vector, $b \in \mathbb{R}$ is the bias, and $\sigma$ is a nonlinear activation.

> [!info] Key Intuition
> A neuron splits its job in two: the linear part $w^\top x + b$ scores how strongly the input aligns with the weights, and the activation reshapes that score into a useful output (probability, signal strength, etc.).

## Mechanics
- $w^\top x$ is a weighted sum of input coordinates — a linear projection.
- $b$ shifts the decision boundary; without it, the boundary is forced through the origin.
- $\sigma$ injects nonlinearity. Without it, stacking neurons collapses to one linear map.

> [!example]- Worked Example
> With $w = (2, -1)$, $b = 0.5$, $x = (1, 3)$, and $\sigma$ the sigmoid:
> - $w^\top x + b = 2 \cdot 1 + (-1) \cdot 3 + 0.5 = -0.5$
> - $y = \sigma(-0.5) \approx 0.378$

## Significance
Every layer in a neural network is a parallel collection of these neurons. Understanding the single-neuron equation is the foundation for the matrix form $h = \sigma(Wx + b)$ used in real layers.
