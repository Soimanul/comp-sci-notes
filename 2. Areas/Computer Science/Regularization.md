**Tags:** #concept #training #optimization
**Related:** [[Overfitting]], [[Gradient Descent]], [[SLP - Training Schedules & Hyperparameters]]

## Definition
Techniques used to prevent **overfitting** by discouraging the learning of a model that is too complex or too sensitive to noise in the training data.

## Common Types
### 1. [[L2 Regularization]] (Weight Decay)
- **Mechanism**: Adds a penalty term $\lambda \sum w^2$ to the loss function.
- **Effect**: Shrinks weights towards zero (but rarely exactly zero). It ensures no single feature dominates the prediction too heavily.

### 2. [[L1 Regularization]]
- **Mechanism**: Adds a penalty term $\lambda \sum |w|$ to the loss function.
- **Effect**: Promotes **sparsity**. It can drive some weights to exactly zero, effectively performing feature selection.

### 3. Dropout
- **Mechanism**: Randomly "drops" (sets to zero) a percentage of neurons during each training step.
- **Effect**: Prevents neurons from "co-adapting" too much, forcing the network to learn redundant, more robust representations.

## Significance
Regularization shifts the focus from minimizing training error to minimizing **generalization error** (the error on unseen data).
