**Tags:** #concept #reco
**Related:** [[Pairwise Loss]], [[Bayesian Personalized Ranking]], [[Precision@K]], [[NDCG@K]]

## Definition

**Pointwise loss** treats each (user, item) pair independently as a regression or classification problem. The model predicts a score for each item, and the loss is computed per item without reference to other items in the user's ranked list.

> [!info] Key Intuition
> Pointwise learning says: "Predict the rating/click probability for item $i$ for user $u$." It converts ranking into a standard regression (MSE, RMSE) or classification (cross-entropy, logistic) problem.

## Examples

| Loss | Setting | Formula |
|---|---|---|
| Mean Squared Error | Rating prediction | $\sum (r_{ui} - \hat{r}_{ui})^2$ |
| Binary cross-entropy | CTR prediction | $-[y\log\hat{p} + (1-y)\log(1-\hat{p})]$ |
| Hinge loss | Binary preference | $\max(0, 1 - y \hat{r})$ |

## Limitations

1. **Independence assumption**: Each item is scored in isolation; the model cannot directly learn "item A should rank above item B for this user"
2. **Label imbalance**: Most (user, item) pairs are unobserved (implicit negative). The model optimises for absolute score values rather than relative ordering
3. **Metric mismatch**: Optimising RMSE does not directly optimise NDCG or Precision@K

> [!warning] Implicit Feedback Problem
> With implicit feedback, pointwise loss requires treating unobserved items as negatives (negative sampling). The choice of how many negatives and how to sample them strongly affects performance.

## When to Use

Pointwise approaches are appropriate when:
- Explicit ratings are available and rating value accuracy matters
- The downstream system uses absolute score thresholds
- Computational simplicity is prioritised

## Significance

Despite its limitations, pointwise loss is widely used in production because of its computational simplicity and ease of integration with standard supervised learning pipelines. Matrix Factorization optimised with MSE is a pointwise approach.
