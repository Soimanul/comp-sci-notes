**Tags:** #concept #ml
**Related:** [[Decision Trees]], [[Random Forest]], [[XGBoost]], [[LightGBM]]

## Definition

**Gradient Boosting Decision Trees (GBDT)** is an ensemble method that builds trees **sequentially**, where each new tree is fit to the **negative gradient** (pseudo-residuals) of the loss function with respect to the current ensemble's predictions.

> [!info] Key Intuition
> Instead of building trees in parallel (like Random Forest), GBDT builds each new tree to correct the errors of the existing ensemble. The negative gradient tells each tree which examples need more attention and in which direction to move predictions.

## Algorithm

**Input:** Training data $\{(x_i, y_i)\}$, differentiable loss $L$, number of trees $M$, learning rate $\eta$

1. Initialise: $F_0(x) = \arg\min_c \sum L(y_i, c)$ (constant prediction)
2. For $m = 1, \ldots, M$:
   - Compute pseudo-residuals: $r_{im} = -\frac{\partial L(y_i, F(x_i))}{\partial F(x_i)}\bigg|_{F=F_{m-1}}$
   - Fit a tree $h_m$ to the pseudo-residuals $\{r_{im}\}$
   - Update: $F_m(x) = F_{m-1}(x) + \eta \cdot h_m(x)$

## Pseudo-Residuals for Common Losses

| Loss | $L(y, \hat{y})$ | Pseudo-residual |
|---|---|---|
| MSE | $\frac{1}{2}(y-\hat{y})^2$ | $y - \hat{y}$ (actual residual) |
| Log-loss | $-[y\log\hat{p} + (1-y)\log(1-\hat{p})]$ | $y - \hat{p}$ (actual − predicted probability) |

## Regularisation

- **Learning rate** $\eta$ (shrinkage): small $\eta$ requires more trees but generalises better
- **Subsample**: train each tree on a random fraction of data (stochastic gradient boosting)
- **Max depth**: typically 3–8 in contrast to Random Forest's full-depth trees

> [!warning] Overfitting Risk
> GBDT can overfit with too many trees or too high a learning rate. Early stopping (monitor validation loss) is the standard mitigation.

## Significance

GBDT is the dominant algorithm for structured/tabular data in production. XGBoost and LightGBM are optimised implementations that win most tabular ML competitions.
