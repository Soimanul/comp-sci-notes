**Tags:** #concept #nlp #ml #svm
**Related:** [[Maximum Margin Classifier]], [[Support Vector Machines]]

## Definition

Support vectors are the subset of training points that lie exactly on the margin boundaries (at distance $\frac{1}{\|\mathbf{w}\|}$ from the hyperplane). They are the only data points that influence the learned decision boundary.

> [!info] Key Intuition
> Delete all non-support-vector points from the training set and retrain — you get exactly the same model. The SVM solution is determined entirely by the hard cases on the boundary.

## Core Mechanics

In the dual formulation, the weight vector is expressed as:
$$\mathbf{w} = \sum_{i} \alpha_i y_i \mathbf{x}_i$$

For non-support vectors, the Lagrange multiplier $\alpha_i = 0$, so they contribute nothing to $\mathbf{w}$. Only support vectors have $\alpha_i > 0$.

This **sparsity** has two practical consequences:
1. **Memory efficiency**: only support vectors need to be stored at prediction time
2. **Sensitivity**: the model is determined only by the most ambiguous points near the boundary

> [!example]- Worked Example
> A dataset of 1,000 emails (spam/ham). After training, only 23 are support vectors — the rest have $\alpha_i = 0$. Predictions use dot products with only these 23 vectors.
