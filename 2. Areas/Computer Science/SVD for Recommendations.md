**Tags:** #concept #reco
**Related:** [[Matrix Factorization]], [[Latent Factors]], [[ALS Algorithm]]

## Definition

**SVD for Recommendations** (also called Funk SVD or regularised SVD) is a matrix factorization model that extends the basic inner product prediction $\hat{r}_{ui} = q_i^T p_u$ by adding **bias terms** to capture systematic rating tendencies of users and items.

> [!info] Key Intuition
> Some users always rate high; some items are universally liked or disliked. Bias terms absorb these systematic effects, leaving the latent factors to model only the user-item interaction signal.

## Model

$$\hat{r}_{ui} = \mu + b_u + b_i + q_i^T p_u$$

where:
- $\mu$ = global average rating across all (user, item) pairs
- $b_u$ = user bias (how much user $u$ rates above/below average)
- $b_i$ = item bias (how much item $i$ is rated above/below average)
- $q_i^T p_u$ = latent factor interaction term

## Objective Function

$$\min \sum_{(u,i) \in K} \left( r_{ui} - \mu - b_u - b_i - q_i^T p_u \right)^2 + \lambda \left( b_u^2 + b_i^2 + \|q_i\|^2 + \|p_u\|^2 \right)$$

## SGD Update Rules

Define the prediction error: $e_{ui} = r_{ui} - \hat{r}_{ui}$

For each observed rating, update:

$$b_u \leftarrow b_u + \gamma (e_{ui} - \lambda b_u)$$
$$b_i \leftarrow b_i + \gamma (e_{ui} - \lambda b_i)$$
$$p_u \leftarrow p_u + \gamma (e_{ui} q_i - \lambda p_u)$$
$$q_i \leftarrow q_i + \gamma (e_{ui} p_u - \lambda q_i)$$

where $\gamma$ = learning rate.

> [!example]- Bias Correction
> Global average $\mu = 3.5$. User A tends to rate 0.5 above average ($b_A = +0.5$). Movie X tends to be rated 0.3 below average ($b_X = -0.3$).
> Baseline prediction for A on X: $3.5 + 0.5 - 0.3 = 3.7$. The latent factor term adjusts this further based on the specific user-item fit.

> [!warning] Naming Confusion
> "SVD for recommendations" is NOT the same as the mathematical Singular Value Decomposition. It is a regularised factorization solved by SGD, popularised by Simon Funk during the Netflix Prize. The name stuck despite the mathematical inaccuracy.

## Significance

Adding bias terms consistently improves RMSE over plain matrix factorization. SVD is the workhorse algorithm for explicit feedback scenarios and is available in libraries like Surprise (Python).
