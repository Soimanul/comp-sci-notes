**Tags:** #concept #reco #ml
**Related:** [[Offline vs Online Metrics]], [[Mean Squared Error (MSE)]]

## Definition

**Mean Absolute Error (MAE)** is a rating metric that measures the average magnitude of errors in predicted ratings, without squaring them.

$$\text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |r_i - \hat{r}_i|$$

where $r_i$ is the true rating and $\hat{r}_i$ is the predicted rating.

> [!info] Key Intuition
> MAE is the average absolute prediction error. If your MAE is 0.5 on a 1–5 scale, the model's rating predictions are off by half a star on average.

## MAE vs RMSE

| Property | MAE | RMSE |
|---|---|---|
| Formula | Mean of $\|error\|$ | Root mean of $error^2$ |
| Outlier sensitivity | **Lower** — treats all errors equally | **Higher** — large errors are penalised more |
| Interpretability | More intuitive (true average error) | Less intuitive (weighted by variance) |
| Common use | When all errors matter equally | When large errors are particularly bad |

> [!example]- Example
> True ratings: [4, 3, 5, 2]. Predictions: [3.5, 3.2, 4.8, 2.5].
> Absolute errors: [0.5, 0.2, 0.2, 0.5]. MAE = (0.5+0.2+0.2+0.5)/4 = **0.35**

> [!warning] Common Misconception
> MAE and [[Mean Squared Error (MSE)]] are only meaningful when the task is **rating prediction** (regression). For ranking tasks, use [[Precision@K]], [[Recall@K]], [[NDCG@K]], or [[MAP@K]].

## Significance

MAE is a better estimator of true average error than RMSE when the error distribution contains outliers. It is commonly used alongside RMSE for recommendation rating evaluation on datasets like MovieLens.
