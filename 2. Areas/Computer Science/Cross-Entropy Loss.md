**Tags:** #concept #math #loss-functions
**Related:** [[Softmax Function]], [[Logistic Loss]], [[SLP - Improving MLPs & Activation Functions]]

## Definition
A loss function used to measure the performance of a classification model whose output is a probability value between 0 and 1.

## Formula (Multi-class)
$$\mathcal{L} = -\sum_{c=1}^M y_{o,c} \log(\hat{y}_{o,c})$$
Where:
- $y$ is a binary indicator if class label $c$ is the correct classification for observation $o$ (if the true class is this one).
- $\hat{y}$ is the predicted probability.

## Why it is used
- **Information Theory**: Measures the cross-entropy between the true distribution and the predicted distribution.

- **Gradients**: Produces much stronger gradients for incorrect predictions compared to [[Mean Squared Error (MSE)]], preventing the training from stalling (vanishing gradients) early on.
