**Tags:** #concept #ml
**Related:** [[Gini Index]], [[Entropy for Decision Trees]], [[Random Forest]], [[Gradient Boosting Decision Trees]]

## Definition

A **Decision Tree** is a hierarchical, non-parametric supervised learning model that partitions the input space by recursively splitting on the feature value that best separates the training examples.

> [!info] Key Intuition
> At each node, the algorithm greedily selects the feature and threshold that create the purest possible child nodes (all same class in one child). This is repeated until a stopping criterion is met (max depth, min samples, or pure leaf).

## Algorithm (CART)

**Training (recursive splitting):**
1. At each node, for every feature and every candidate threshold, compute the impurity reduction (Gini or information gain).
2. Choose the split that maximises impurity reduction.
3. Recurse on each child until stopping criterion met.
4. Assign each leaf the majority class (classification) or mean target value (regression).

**Prediction:** traverse the tree by evaluating splits until reaching a leaf.

## Splitting Criteria

| Criterion | Used For | Formula |
|---|---|---|
| [[Gini Index]] | Classification | $\sum_k p_k(1-p_k)$ |
| [[Entropy for Decision Trees]] | Classification | $-\sum_k p_k \log_2 p_k$ |
| Variance reduction | Regression | Variance of targets in node |

## Pros and Cons

| Pros | Cons |
|---|---|
| Highly interpretable (can be visualised) | High variance — small data changes produce different trees |
| No feature scaling needed | Prone to overfitting (grows until leaves are pure) |
| Handles mixed feature types | Cannot extrapolate beyond training data range |
| Fast inference (log depth) | Ignores feature interactions across branches |

> [!warning] Overfitting
> Fully grown trees memorise training data. In practice, trees are pruned (max_depth, min_samples_split, min_impurity_decrease) or used as weak learners inside [[Random Forest]] or [[Gradient Boosting Decision Trees]].

## Significance

Decision Trees are the foundation of the most successful tabular learning algorithms in production: Random Forest and Gradient Boosted Decision Trees (XGBoost, LightGBM).
