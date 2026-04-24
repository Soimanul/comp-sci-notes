**Tags:** #concept #ml
**Related:** [[Decision Trees]], [[Gradient Boosting Decision Trees]], [[XGBoost]], [[LightGBM]]

## Definition

**Random Forest** is an ensemble method that builds many decorrelated decision trees using **bagging** (bootstrap aggregating) and **random feature subsampling**, then aggregates their predictions by majority vote (classification) or averaging (regression).

> [!info] Key Intuition
> A single decision tree has high variance — it overfits to training data. Averaging many trees reduces variance without increasing bias, as long as the trees are decorrelated. Random feature subsampling is the key mechanism that decorrelates the trees.

## Algorithm

1. For $t = 1, \ldots, T$:
   - Sample $n$ training points **with replacement** (bootstrap sample)
   - Grow a full decision tree, but at each split consider only $m$ randomly chosen features ($m \approx \sqrt{d}$ for classification, $m \approx d/3$ for regression)
2. Prediction: average (regression) or majority vote (classification) over all $T$ trees

## Why It Works: Bias–Variance

| Component | Effect |
|---|---|
| Full-depth trees | Low bias (each tree fits training data well) |
| Bagging + averaging | Reduces variance by $\frac{1}{T}$ for uncorrelated trees |
| Random feature subsampling | Decorrelates trees (correlation $\rho$ reduces variance benefit) |

Variance of the ensemble: $\rho \sigma^2 + \frac{1-\rho}{T} \sigma^2$. As $T \to \infty$, variance approaches $\rho \sigma^2$.

## Hyperparameters

| Parameter | Effect |
|---|---|
| `n_estimators` (T) | More trees = lower variance, diminishing returns |
| `max_features` (m) | Smaller = more decorrelated, but weaker individual trees |
| `max_depth` | Controls per-tree bias |

> [!example]- Out-of-Bag (OOB) Error
> Each bootstrap sample excludes ~37% of training points. Those excluded samples can be used to estimate test error without a separate validation set — this is the **out-of-bag error**, a free cross-validation estimate built into Random Forest.

## Significance

Random Forest is one of the most robust and widely-used ML algorithms, performing well on tabular data out of the box with little tuning. It also provides built-in feature importance estimates and OOB error.
