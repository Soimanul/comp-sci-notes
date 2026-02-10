**Tags:** #concept #preprocessing
**Related:** [[k-Nearest Neighbors]], [[Gradient Descent]], [[SLP - Introduction & kNN]]

## Definition
The process of rescaling the features of a dataset so they share a common scale, typically $[0, 1]$ or a mean of 0 and standard deviation of 1.

## Why it is Mandatory
1. **Distance-Based Models**: Algorithms like [[k-Nearest Neighbors]] rely on Euclidean distance. If one feature (e.g., Salary) has a range of 0–100,000 and another (e.g., Age) is 0–100, the salary will dominate the distance calculation regardless of its actual importance.
2. **Optimization Stability**: In [[Gradient Descent]], unnormalized features create an "elongated" loss landscape (narrow canyons). This forces the optimizer to use a very small learning rate to avoid oscillating, slowing down convergence.

## Common Techniques
- **Min-Max Scaling**: $x' = \frac{x - \min}{\max - \min}$. Rescales to $[0, 1]$.
- **Standardization (Z-score)**: $x' = \frac{x - \mu}{\sigma}$. Centers data around 0 with unit variance.

## Significance
Normalization ensures that the model treats all features with appropriate relative importance and accelerates the training of neural networks.
