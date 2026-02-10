**Tags:** #concept #training #neural-networks
**Related:** [[SLP - Improving MLPs & Activation Functions]], [[Gradient Descent]], [[Backpropagation]]

## Definition
The strategy used to set the starting values of the weights in a neural network before training begins.

## The Symmetry Breaking Problem
If all weights are initialized to the same value (e.g., $W=0$ or $W=1$):
- Every neuron in a hidden layer will receive the same input.
- During [[Backpropagation]], every neuron will receive the same gradient update.
- Consequently, all neurons in a layer will learn the exact same feature, effectively collapsing the layer into a single neuron. **Random initialization** is required to break this symmetry.

## Stability: Vanishing & Exploding Gradients
- **Exploding**: If weights are too large, signals multiply and grow exponentially, causing the training to diverge.
- **Vanishing**: If weights are too small (especially with Sigmoid), signals shrink to zero, and the network stops learning.

## Standard Strategies (Rules of Thumb)
1. **Xavier (Glorot) Initialization**: Best for **Sigmoid** or **Tanh** activations. It keeps the variance of activations and gradients constant across layers.
2. **He Initialization**: Specifically designed for **[[ReLU]]**. It accounts for the fact that ReLU "kills" half the signal (negative domain) by doubling the initialization variance.

## Significance
Proper initialization ensures that the signal can flow deep into the network during the forward pass and that gradients can flow back to the first layers during the backward pass.