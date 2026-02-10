**Tags:** #concept #training #optimization
**Related:** [[Learning Rate Schedules]], [[SLP - Training Schedules & Hyperparameters]]

## Definition
The process of searching for the optimal set of hyperparameters (parameters not learned by the model itself, like learning rate or $k$ in kNN).

## Strategies
- **Grid Search**: Trying every combination of values (expensive).
- **Random Search**: Sampling values randomly. Often more effective as some parameters (like learning rate) typically matter more than others.
- **Cross-Validation**: Evaluating each set of parameters on a validation set to ensure generalization.
