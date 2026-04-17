**Tags:** #concept #nlp #ml #svm
**Related:** [[Support Vector Machines]], [[Slack Variables]], [[Maximum Margin Classifier]]

## Definition

The soft-margin SVM relaxes the hard-margin constraint to allow some misclassifications, controlled by a regularisation parameter $C$. It trades margin width against training error, enabling application to real-world, non-linearly-separable data.

> [!info] Key Intuition
> $C$ is the "cost of being wrong": large $C$ tolerates little error and risks overfitting; small $C$ allows more violations and risks underfitting. $C$ is the primary hyperparameter to tune.

## Core Mechanics

**Primal optimisation** (soft margin):
$$\min_{\mathbf{w}, b, \boldsymbol{\xi}} \frac{1}{2}\|\mathbf{w}\|^2 + C \sum_{i} \xi_i$$
$$\text{subject to } y_i(\mathbf{w} \cdot \mathbf{x}_i + b) \geq 1 - \xi_i, \quad \xi_i \geq 0 \; \forall i$$

- $\xi_i = 0$: point correctly classified with margin $\geq 1$
- $0 < \xi_i \leq 1$: correctly classified but inside the margin
- $\xi_i > 1$: misclassified

The $C\sum\xi_i$ term penalises violations; $\frac{1}{2}\|\mathbf{w}\|^2$ maximises the margin. $C$ balances these objectives.

> [!example]- Worked Example
> Text classification with noisy labels. With $C = 100$, the model over-fits to mislabelled examples. With $C = 0.01$, it finds a wider margin and generalises better on the test set.

> [!warning] Common Misconception
> A higher $C$ does not always mean a "better" model. On noisy data, very high $C$ forces the model to correctly classify outliers at the cost of a tiny, fragile margin — the opposite of what SVMs are designed to achieve.
