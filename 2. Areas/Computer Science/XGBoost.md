**Tags:** #concept #ml
**Related:** [[Gradient Boosting Decision Trees]], [[LightGBM]], [[Decision Trees]]

## Definition

**XGBoost** (eXtreme Gradient Boosting, Chen & Guestrin 2016) is an optimised GBDT implementation that adds **second-order Taylor expansion of the loss**, explicit **tree regularisation** terms, and a **column/row subsampling** strategy to achieve strong accuracy and fast training.

> [!info] Key Intuition
> Standard GBDT fits each tree to first-order pseudo-residuals. XGBoost uses both the gradient (first derivative) and the Hessian (second derivative) of the loss to compute optimal leaf weights analytically, resulting in more precise updates.

## Objective Function

At step $m$, XGBoost minimises:

$$\mathcal{L}^{(m)} = \sum_{i=1}^{n} \left[ g_i f_m(x_i) + \frac{1}{2} h_i f_m(x_i)^2 \right] + \Omega(f_m)$$

where:
- $g_i = \partial_{\hat{y}} L(y_i, \hat{y}_i^{(m-1)})$ — first-order gradient
- $h_i = \partial^2_{\hat{y}} L(y_i, \hat{y}_i^{(m-1)})$ — second-order Hessian
- $\Omega(f) = \gamma T + \frac{1}{2}\lambda \|w\|^2$ — regularisation ($T$ = number of leaves, $w$ = leaf weights)

## Optimal Leaf Weight

For a leaf $j$ containing instances $I_j$:

$$w_j^* = -\frac{\sum_{i \in I_j} g_i}{\sum_{i \in I_j} h_i + \lambda}$$

## Split Gain

$$\text{Gain} = \frac{1}{2} \left[ \frac{G_L^2}{H_L + \lambda} + \frac{G_R^2}{H_R + \lambda} - \frac{(G_L + G_R)^2}{H_L + H_R + \lambda} \right] - \gamma$$

where $G = \sum g_i$, $H = \sum h_i$ for the respective child nodes. The $-\gamma$ term is the regularisation penalty for adding a leaf.

## Key Hyperparameters

| Parameter | Role |
|---|---|
| `n_estimators` | Number of trees |
| `max_depth` | Maximum tree depth |
| `learning_rate` (η) | Shrinkage |
| `subsample` | Row subsampling fraction |
| `colsample_bytree` | Column subsampling fraction |
| `lambda` (L2) | Leaf weight regularisation |
| `gamma` | Minimum gain to split |

## Significance

XGBoost dominated machine learning competitions (Kaggle) for several years after its release. It remains one of the top-performing algorithms for tabular data and CTR prediction tasks in recommendation.
