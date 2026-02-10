**Tags:** #concept #neural-networks
**Related:** [[Activation Functions]], [[SLP - Improving MLPs & Activation Functions]]

## Definition
Rectified Linear Unit (ReLU) is a non-linear activation function that outputs the input directly if it is positive, and zero otherwise.

## Formula
$$f(z) = \max(0, z)$$

## Advantages
- **Computational Efficiency**: Only requires a simple comparison.
- **Gradient Flow**: Does not saturate in the positive domain, unlike [[Sigmoid Function]], which helps mitigate the vanishing gradient problem.

## Disadvantages
- **Dead ReLU Problem**: If a neuron's weights are adjusted such that it always outputs zero (negative input range), it will never fire again because its gradient is zero.
