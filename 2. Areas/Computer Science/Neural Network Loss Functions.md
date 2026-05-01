**Tags:** #concept #neural-networks #training
**Related:** [[Cross-Entropy Loss]], [[Backpropagation]], [[Neural Network Optimizers]]

## Definition
A loss function $L(\theta)$ quantifies how badly the network's predictions disagree with the targets. Training minimizes $L$ with respect to the parameters $\theta$. The choice of loss must match the task: classification, regression, or ranking.

> [!info] Key Intuition
> The loss function is the "objective" the optimizer climbs down. Pick the wrong loss and even a perfect optimizer learns the wrong thing.

## Common Choices

| Task | Loss | When to use |
|---|---|---|
| Binary classification | Binary cross-entropy | Output is a single probability $\in (0,1)$ |
| Multi-class classification | Categorical cross-entropy | Output is a softmax over $K$ classes |
| Regression | Mean Squared Error (MSE) | Continuous-valued targets |
| Regression with outliers | Mean Absolute Error (MAE) / Huber | Robust to extreme values |
| Ranking | Pairwise / listwise losses | Order matters more than absolute scores |

## Cross-Entropy Form
For multi-class classification with one-hot label $y$ and predicted softmax distribution $p$:
$$L(\theta) = -\frac{1}{N} \sum_{i=1}^{N} \sum_{k=1}^{K} y_{ik} \log p_{ik}$$

> [!warning] Common Misconception
> MSE works for classification mathematically but converges much more slowly than cross-entropy because its gradient is small when the model is confidently wrong. Always prefer cross-entropy for classification.

## Significance
Together with the optimizer and the architecture, the loss defines what "good" means during training. Wrong loss → the model learns a different problem than the one you intended.
