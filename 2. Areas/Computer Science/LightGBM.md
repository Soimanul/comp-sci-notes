**Tags:** #concept #ml
**Related:** [[Gradient Boosting Decision Trees]], [[XGBoost]], [[Decision Trees]]

## Definition

**LightGBM** (Light Gradient Boosting Machine, Microsoft 2017) is a highly optimised GBDT implementation featuring two key innovations: **Gradient-based One-Side Sampling (GOSS)** and **Exclusive Feature Bundling (EFB)**, plus a leaf-wise (best-first) tree growth strategy.

> [!info] Key Intuition
> Standard GBDT scans all data for all features at every split. LightGBM makes this dramatically faster by: (1) skipping low-gradient training examples (GOSS), (2) bundling mutually exclusive sparse features into one (EFB), and (3) growing the leaf with the largest loss reduction first.

## Key Innovations

### 1. Gradient-based One-Side Sampling (GOSS)

Keep all instances with large gradients (large errors — more informative). Randomly sample a fraction $b$ of instances with small gradients. This preserves most of the information while reducing data size.

### 2. Exclusive Feature Bundling (EFB)

Many features in high-dimensional data are mutually exclusive (never non-zero simultaneously, e.g. one-hot encoded categoricals). EFB bundles these into single features, reducing the effective number of features and thus the histogram construction cost.

### 3. Leaf-Wise Growth

| Strategy | Description | Behaviour |
|---|---|---|
| Level-wise (XGBoost default) | Grow all leaves at same depth | Balanced, predictable |
| Leaf-wise (LightGBM) | Always split the leaf with maximum loss reduction | Deeper asymmetric trees; lower loss for same number of leaves |

> [!warning] Overfitting with Leaf-Wise Growth
> Leaf-wise growth can overfit on small datasets. Key hyperparameters to control this: `num_leaves`, `min_data_in_leaf`, `lambda_l1`, `lambda_l2`.

## Comparison to XGBoost

| Feature | LightGBM | XGBoost |
|---|---|---|
| Tree growth | Leaf-wise | Level-wise (default) |
| Categorical features | Native support | Requires encoding |
| Speed | Faster (GOSS + EFB) | Slightly slower |
| Memory | Lower (histogram-based) | Higher |

## Significance

LightGBM is the go-to GBDT implementation for large-scale tabular data in production and competitions, offering 10–20× speedup over vanilla GBDT while achieving comparable or better accuracy.
