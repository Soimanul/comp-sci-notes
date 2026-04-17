**Tags:** #concept #nlp #ml #svm
**Related:** [[Support Vector Machines]], [[Kernel Trick]], [[Support Vectors]]

## Definition

The SVM dual formulation re-expresses the primal constrained optimisation in terms of Lagrange multipliers $\alpha_i$, one per training example. The dual enables the kernel trick and yields sparse solutions where only support vectors have $\alpha_i > 0$.

> [!info] Key Intuition
> The dual trades $p$ primal variables (weight vector dimensionality) for $n$ dual variables (one per training point). When $p \gg n$ (e.g., text features), solving the dual is dramatically cheaper.

## Core Mechanics

**Dual objective** (maximise):
$$\mathcal{L}(\boldsymbol{\alpha}) = \sum_i \alpha_i - \frac{1}{2}\sum_i\sum_j \alpha_i \alpha_j y_i y_j K(\mathbf{x}_i, \mathbf{x}_j)$$
subject to $\alpha_i \geq 0$ and $\sum_i \alpha_i y_i = 0$.

For soft-margin SVM, the box constraint becomes $0 \leq \alpha_i \leq C$.

KKT complementary slackness: $\alpha_i(y_i f(\mathbf{x}_i) - 1) = 0$, so:
- $\alpha_i = 0$ → non-support vector (no contribution)
- $0 < \alpha_i < C$ → on the margin (support vector)
- $\alpha_i = C$ → inside the margin or misclassified

> [!example]- Worked Example
> Bag-of-words feature space has $d = 50{,}000$ dimensions but only $n = 500$ training documents. Solving the dual requires optimising over 500 variables rather than 50,000.
