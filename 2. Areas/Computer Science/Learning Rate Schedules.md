**Tags:** #concept #training #optimization
**Related:** [[Gradient Descent]], [[Hyperparameter Tuning]]

## Definition
A predefined strategy for adjusting the learning rate during the training process.

## Common Schedules
- **Step Decay**: Reducing the learning rate by a factor every few epochs.
- **Cosine Annealing**: Gradually decreasing the rate following a cosine curve.
- **Linear Warmup**: Starting with a small rate and increasing it to the initial value to stabilize early training.

## Significance
Allows for fast progress at the start of training with a large learning rate, while ensuring convergence to a fine-tuned minimum at the end.
