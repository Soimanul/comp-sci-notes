**Tags:** #concept #nlp #ml #svm
**Related:** [[Support Vector Machines]], [[Support Vectors]], [[SVM Dual Formulation]]

## Definition

The maximum-margin classifier finds the hyperplane that separates two classes while maximising the distance (margin) between the hyperplane and the nearest data points of each class. The margin is $\frac{2}{\|\mathbf{w}\|}$ for a hyperplane parameterised by $\mathbf{w}$.

> [!info] Key Intuition
> Among all legal separating hyperplanes, the one farthest from all points is the most confident and generalises best — small perturbations in the data are unlikely to flip predictions.

## Core Mechanics

**Decision function**: $f(\mathbf{x}) = \text{sign}(\mathbf{w} \cdot \mathbf{x} + b)$

**Primal optimisation** (hard margin):
$$\min_{\mathbf{w}, b} \frac{1}{2}\|\mathbf{w}\|^2 \quad \text{subject to } y_i(\mathbf{w} \cdot \mathbf{x}_i + b) \geq 1 \; \forall i$$

- Minimising $\|\mathbf{w}\|^2$ is equivalent to maximising the margin $\frac{2}{\|\mathbf{w}\|}$
- Constraints enforce correct classification with margin $\geq 1$
- Only support vectors (points exactly on the margin boundaries) influence $\mathbf{w}$

> [!example]- Worked Example
> Two classes in 2D, linearly separable. Three data points lie exactly on the margin boundaries — these are the support vectors. Removing any non-support-vector point leaves the hyperplane unchanged. Removing a support vector shifts the margin.

> [!warning] Common Misconception
> The hard-margin SVM fails entirely when data is not linearly separable — even a single outlier makes the problem infeasible. The soft-margin extension (introducing slack variables) is required for real-world data.
