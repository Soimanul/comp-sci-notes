**Tags:** #concept #nlp #ml #svm
**Related:** [[Soft Margin SVM]], [[Support Vector Machines]]

## Definition

Slack variables $\xi_i \geq 0$ are introduced in the soft-margin SVM to allow training points to violate the margin constraint. Each $\xi_i$ measures the degree of violation: zero means correctly classified with full margin, and $\xi_i > 1$ means misclassified.

> [!info] Key Intuition
> Slack variables are the "error budget" of the SVM: they let the model say "I'll accept this mistake, but at a cost of $C \cdot \xi_i$ in the objective."

## Core Mechanics

Three cases by $\xi_i$ value:
- $\xi_i = 0$: point on or outside the margin boundary — no violation
- $0 < \xi_i \leq 1$: inside the margin but on the correct side of the hyperplane
- $\xi_i > 1$: on the wrong side — a true misclassification

The total penalty is $C \sum_i \xi_i$ added to the primal objective. This term competes with the margin-maximisation term $\frac{1}{2}\|\mathbf{w}\|^2$.

> [!example]- Worked Example
> A training point from class +1 ends up on the wrong side: $y_i f(\mathbf{x}_i) = -0.3$, so $\xi_i = 1.3$. With $C = 1$, this single point contributes 1.3 to the objective penalty — incentivising the model to correct it if the margin cost is acceptable.
