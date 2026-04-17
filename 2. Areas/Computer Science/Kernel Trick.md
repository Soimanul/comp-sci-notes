**Tags:** #concept #nlp #ml #svm
**Related:** [[Support Vector Machines]], [[Kernel Functions]], [[SVM Dual Formulation]]

## Definition

The kernel trick replaces explicit computation of high-dimensional (or infinite-dimensional) feature maps $\phi(\mathbf{x})$ with a kernel function $K(\mathbf{x}_i, \mathbf{x}_j) = \phi(\mathbf{x}_i) \cdot \phi(\mathbf{x}_j)$ computed directly in the original space. This allows SVMs to learn non-linear boundaries efficiently.

> [!info] Key Intuition
> The SVM dual only ever needs dot products between data points — never the coordinates themselves. A kernel function computes that dot product in a transformed space without ever going there.

## Core Mechanics

The dual SVM decision function:
$$f(\mathbf{x}) = \text{sign}\!\left(\sum_i \alpha_i y_i K(\mathbf{x}_i, \mathbf{x}) + b\right)$$

Common kernels:
| Kernel | Formula | Feature Space |
|---|---|---|
| Linear | $\mathbf{x}_i \cdot \mathbf{x}_j$ | original space |
| Polynomial (degree $d$) | $(\mathbf{x}_i \cdot \mathbf{x}_j + c)^d$ | degree-$d$ monomials |
| RBF / Gaussian | $\exp\!\left(-\gamma\|\mathbf{x}_i - \mathbf{x}_j\|^2\right)$ | infinite-dimensional |

Kernels must satisfy Mercer's theorem: the kernel matrix must be positive semi-definite.

> [!example]- Worked Example
> XOR problem: not linearly separable in 2D. With an RBF kernel, the SVM implicitly projects into infinite dimensions and finds a separating hyperplane — without computing a single infinite-dimensional coordinate.

> [!warning] Common Misconception
> The kernel trick is not "projecting data to a higher dimension." No data ever moves — only the inner product computation changes. The transformation $\phi$ need never be constructed explicitly.
