**Tags:** #topic #hub #nlp
**Related:** [[Natural Language Processing]], [[Text Classification]], [[Maximum Entropy Classifier]]

## Overview
Logistic Regression is a central model for text classification in NLP. While it can be seen as a simple neural unit, in this course it is framed as a **Maximum Entropy Classifier**: a probabilistic model that makes the weakest possible assumptions while remaining consistent with observed data.

## Knowledge Map
### 1. Conceptual Foundations
- [[Maximum Entropy Classifier]]
- [[Entropy (in Information Theory)]]

### 2. The Model
- [[Sigmoid Function]]
- [[Log-Odds]]
- [[Feature Functions]]

### 3. Training

- [[Cross-Entropy Minimization]]
- [[Gradient Descent]]

## Mechanics

1. **Compute Score**: $z = \mathbf{w}^T \mathbf{x} + b$ (see [[Log-Odds]]).

2. **Apply Sigmoid**: $\hat{y} = \sigma(z) = \frac{1}{1+e^{-z}}$ (see [[Sigmoid Function]]).

3. **Decision Rule**: Typically, we assign Class 1 if $\hat{y} > 0.5$ (or $z > 0$).

## Significance
Unlike the Perceptron, Logistic Regression provides a measure of certainty (probability) and can be optimized using gradient-based methods even when data is not perfectly separable. In NLP, it is often referred to as a Maximum Entropy classifier, emphasizing its role in making unbiased probabilistic predictions.
