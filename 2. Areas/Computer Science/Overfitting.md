**Tags:** #concept #training #machine-learning
**Related:** [[Regularization]], [[Hyperparameter Tuning]], [[k-Nearest Neighbors]]

## Definition
Overfitting occurs when a model learns the "noise" in the training data rather than the underlying pattern, leading to poor performance on new, unseen data.

## The Bias-Variance Tradeoff
- **Overfitting (High Variance)**: The model is too complex (e.g., $k=1$ in [[k-Nearest Neighbors]]). It fits the training data perfectly but fails to generalize.
- **Underfitting (High Bias)**: The model is too simple (e.g., a straight line for curved data). It misses the underlying trend entirely.

## Detection
Overfitting is typically identified when the **Training Loss** continues to decrease while the **Validation/Test Loss** starts to increase.

## Prevention
- **[[Regularization]]**: Penalizing complexity (L1/L2).
- **Early Stopping**: Halting training when validation loss stops improving.
- **More Data**: Increasing the sample size helps the model distinguish signal from noise.
- **Dropout**: For neural networks.
