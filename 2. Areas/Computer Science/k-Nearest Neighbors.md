**Tags:** #concept #algorithm #knn
**Related:** [[SLP - Introduction & kNN]], [[Minkowski Distance]], [[Supervised Learning]]

## Definition
k-Nearest Neighbors (kNN) is a non-parametric, lazy learning algorithm used for both classification and regression. It predicts the label of a query point based on the $k$ closest training examples in the feature space.

## Mechanism
1. **Store Data**: The algorithm simply stores all training examples.
2. **Calculate Distance**: When a new point arrives, calculate its distance (usually [[Minkowski Distance]] with $p=2$) to all stored points.
3. **Find Neighbors**: Identify the $k$ nearest points.
4. **Vote/Average**: 
   - **Classification**: Majority vote of the neighbors.
   - **Regression**: Average of the neighbor values.

## Geometric Interpretation
### Voronoi Tesselation
The decision boundaries of a 1-Nearest Neighbor algorithm can be visualized as a **Voronoi Tesselation**. Each training point occupies a "cell" where any point within that cell is closer to that specific training point than any other. As $k$ increases, these jagged boundaries become smoother.

## The Tradeoff of $k$
Choosing the number of neighbors is a classic **Bias-Variance Tradeoff**:
- **$k=1$ (High Variance / Low Bias)**: The model is extremely sensitive to individual points and noise (Overfitting). The boundary is complex and follows every detail of the training data.
- **$k=N$ (Low Variance / High Bias)**: The model simply predicts the majority class of the entire dataset regardless of the input (Underfitting). The boundary is effectively non-existent.

## Practical Considerations
- **Choosing $k$**: Optimized by minimizing validation error. 
- **Feature Scaling**: Crucial because distance is scale-dependent. Unscaled features with large ranges will dominate the metric. See [[Normalization (Data)]].
- **Curse of Dimensionality**: As dimensions increase, points become sparse and "equally far" from each other, breaking the local heuristic.
