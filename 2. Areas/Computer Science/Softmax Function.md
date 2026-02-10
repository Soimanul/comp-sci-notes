**Tags:** #concept #math #neural-networks
**Related:** [[Sigmoid Function]], [[Cross-Entropy Loss]], [[SLP - Multi-class Classification & Optimization]]

## Definition
An activation function that generalizes the [[Sigmoid Function]] to multiple classes. It squashes a vector of $K$ real numbers (scores) into a probability distribution that sums to 1.

## Mathematical Formula
For a vector $\mathbf{z}$:
$$\sigma(\mathbf{z})_i = \frac{e^{z_i}}{\sum_{j=1}^K e^{z_j}}$$

## Properties
- **Mutual Exclusivity**: Since outputs sum to 1, increasing the probability of one class decreases the others.
- **Scale Invariance**: Softmax is invariant to constant shifts in input (e.g., subtracting the maximum score for numerical stability).

## Usage
Used almost exclusively in the **output layer** of multi-class classification networks.
