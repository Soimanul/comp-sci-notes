**Tags:** #concept #nlp #ml #svm
**Related:** [[Kernel Trick]], [[Support Vector Machines]]

## Definition

A kernel function $K(\mathbf{x}_i, \mathbf{x}_j)$ computes the dot product between two points in an (implicitly defined) feature space. Valid kernels must satisfy Mercer's theorem: the resulting kernel matrix must be symmetric and positive semi-definite.

> [!info] Key Intuition
> A kernel is a similarity measure that doubles as an inner product in some (possibly infinite-dimensional) space — this equivalence is exactly what the kernel trick exploits.

## Core Mechanics

| Kernel | Formula | Key parameter | Notes |
|---|---|---|---|
| **Linear** | $\mathbf{x}_i^\top\mathbf{x}_j$ | — | Equivalent to no transformation |
| **Polynomial** | $(\mathbf{x}_i^\top\mathbf{x}_j + c)^d$ | degree $d$, offset $c$ | Captures feature interactions |
| **RBF (Gaussian)** | $\exp(-\gamma\|\mathbf{x}_i-\mathbf{x}_j\|^2)$ | bandwidth $\gamma$ | Infinite-dimensional; universal approximator |
| **Sigmoid** | $\tanh(\kappa\,\mathbf{x}_i^\top\mathbf{x}_j + \theta)$ | $\kappa$, $\theta$ | Not always positive semi-definite |
| **String kernel** | varies | — | Common in text; operates on sequences directly |

For NLP, the **linear kernel** often works well because bag-of-words feature spaces are already high-dimensional and linear SVMs are fast to train.

> [!warning] Common Misconception
> Kernel choice is not purely about expressiveness. The RBF kernel can fit any training data if $\gamma$ is large enough — but that over-fits. Kernel selection is a regularisation decision, not just a capacity decision.
