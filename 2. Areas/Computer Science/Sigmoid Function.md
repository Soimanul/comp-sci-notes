**Tags:** #concept #math #neural-networks
**Related:** [[Activation Functions]], [[Logistic Regression]], [[SLP - From Perceptron to Logistic Regression]]

## Definition
A mathematical function that maps any real-valued number into a value between 0 and 1. It is frequently used in binary classification to represent probabilities.

## Formula
$$\sigma(z) = \frac{1}{1 + e^{-z}}$$

## Properties
- **Output Range**: $(0, 1)$.
- **Center**: $\sigma(0) = 0.5$.
- **Derivative**: $\sigma'(z) = \sigma(z)(1 - \sigma(z))$. This simple derivative makes it computationally efficient during [[Backpropagation]].

## Role in SLP
Used to convert the linear score $z = w^T x + b$ into a probability $\hat{y} = P(y=1|x)$, evolving the Perceptron into [[Logistic Regression]].
