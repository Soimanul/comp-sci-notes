**Tags:** #concept #neural-networks 
**Related:** [[Perceptron]], [[Multilayer Perceptron]], [[SLP - Improving MLPs & Activation Functions]]

## Definition
A mathematical function applied to the output of a neuron. It determines whether the neuron should "fire" (activate) by transforming the weighted sum of inputs.

## Purpose
Crucially, non-linear activation functions introduce **non-linearity** to the network. Without them, any number of layers in a neural network collapses into a single linear transformation (a simple dot product), making it incapable of learning complex patterns like XOR.

## Common Functions

### [[Sigmoid Function]]
- **Formula**: $\sigma(z) = \frac{1}{1 + e^{-z}}$
- **Range**: $(0, 1)$. Useful for binary classification.
- **Issue**: Vanishing gradients in deep networks (gradients $\approx 0$ for very large/small inputs).

### [[ReLU]] (Rectified Linear Unit)
- **Formula**: $f(z) = \max(0, z)$
- **Pros**: Cheap to compute, prevents vanishing gradients for $z > 0$.
- **Issue**: "Dead ReLU" - neurons can stop learning if their weights push inputs into the negative domain where the gradient is 0.

### [[Softmax Function]]
- Used in the **output layer** for multi-class classification to produce a probability distribution.

## Comparison Table

| Function | Output Range | Best for... |
| :--- | :--- | :--- |
| **Sigmoid** | $(0, 1)$ | Binary Output layer |
| **ReLU** | $[0, \infty)$ | Hidden layers |
| **Softmax** | $(0, 1)$, $\sum = 1$ | Multi-class Output layer |

## Diagram
![[DeqKjeD6qNmhUNiDfoPBb3xfafw.avif]]
