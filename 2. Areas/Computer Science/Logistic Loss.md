**Tags:** #concept #math #loss-functions
**Related:** [[Logistic Regression]], [[Cross-Entropy Loss]], [[SLP - From Perceptron to Logistic Regression]]

## Definition
The loss function used for training binary classification models like [[Logistic Regression]]. It is the negative log-likelihood of the Bernoulli distribution.

## Formula
For a single point with label $y \in \{0, 1\}$ and prediction $\hat{y}$:
$$\ell = -(y \log(\hat{y}) + (1-y) \log(1-\hat{y}))$$

## Significance
Unlike the squared error used in linear regression, Logistic Loss is convex for logistic regression, ensuring that [[Gradient Descent]] can find the global minimum. It penalizes confident but wrong predictions exponentially.
