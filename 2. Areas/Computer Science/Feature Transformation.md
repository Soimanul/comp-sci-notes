**Tags:** #concept #neural-networks
**Related:** [[SLP - Multi-Layer Perceptrons]], [[Multilayer Perceptron]], [[Activation Functions]]

## Definition
The process of mapping input data from its original space into a new feature space, often of different dimensionality, to make it more suitable for modeling.

## In Neural Networks
Hidden layers in a [[Multilayer Perceptron]] act as automatic feature transformers. They "deform" the input space such that points that were not linearly separable (like XOR) become separable by the output layer.

## Case Study: Polar Coordinates
Consider a dataset with two classes arranged in concentric circles. 
- **Original Space (Cartesian $x, y$)**: No straight line (hyperplane) can separate the inner circle from the outer circle.
- **Transformed Space (Polar $r, \theta$)**: By calculating the radius $r = \sqrt{x^2 + y^2}$, the two classes become separated by a constant value of $r$. In this new 2D space, a simple vertical line can perfectly classify the data.

## Geometric Intuition
A linear transformation can rotate, reflect, scale, and shear space. When combined with a non-linear [[Activation Functions]], the network can perform "folds" or "warps" in space, allowing it to learn complex boundaries.