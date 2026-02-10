**Tags:** #concept #algorithm #optimization
**Related:** [[Gradient Descent]], [[Momentum Gradient Descent]], [[SLP - Multi-class Classification & Optimization]]

## Definition
A variant of [[Gradient Descent]] where the gradient is estimated using a small, randomly selected subset of the data (a mini-batch) rather than the full dataset.

## Intuition: Noise as a Regularizer
In traditional Batch Gradient Descent, the loss curve is smooth and deterministic. In SGD, because each step is based on a random sample, the path is "noisy" and zigzags.

- **Exploration**: This noise allows the optimizer to "jump" out of shallow local minima or flat regions ([[Saddle Points]]) where batch descent might get stuck.

- **Speed**: Since the gradient of a mini-batch is a good approximation of the true gradient, the model can make many more updates in the same amount of time.

## Computational Efficiency

- **Memory**: You only need to fit a mini-batch in GPU memory, not the millions of samples in a typical dataset.
  
- **Stochasticity**: The smaller the batch size, the more stochastic (noisy) the updates.

## Disadvantages
**Noisy Convergence**: The loss does not decrease monotonically; it "zigzags" around the minimum and may never perfectly settle without a [[Learning Rate Schedules]].