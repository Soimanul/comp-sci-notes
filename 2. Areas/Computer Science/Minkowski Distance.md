**Tags:** #concept #math #knn
**Related:** [[k-Nearest Neighbors]], [[SLP - Introduction & kNN]]

## Definition
A generalized distance metric in a normed vector space, which can be seen as a generalization of both Euclidean and Manhattan distance.

## Formula
For two points $X$ and $Y$ in $n$-dimensional space:
$$
D(X, Y) = \left( \sum_{i=1}^n |x_i - y_i|^p \right)^{1/p}
$$

## Special Cases
- **$p=1$**: Manhattan distance (taxicab).
- **$p=2$**: Euclidean distance.
- **$p \to \infty$**: Chebyshev distance (limit equals $\max_i |x_i-y_i|$).
