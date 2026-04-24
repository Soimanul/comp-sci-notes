**Tags:** #concept #reco
**Related:** [[Latent Factors]], [[SVD for Recommendations]], [[ALS Algorithm]], [[Collaborative Filtering]], [[Inner Product Limitation]]

## Definition

**Matrix Factorization (MF)** is a model-based collaborative filtering technique that decomposes the user-item ratings matrix $R$ into two low-rank factor matrices $P$ (users) and $Q$ (items), whose inner product approximates observed ratings.

> [!info] Key Intuition
> Instead of storing the full sparse ratings matrix, MF learns a compact representation of every user and item as a vector of $f$ latent factors. The predicted rating for any user-item pair is simply the dot product of their factor vectors.

## Model

$$\hat{r}_{ui} = q_i^T p_u$$

Where:
- $p_u \in \mathbb{R}^f$ = user $u$'s latent factor vector
- $q_i \in \mathbb{R}^f$ = item $i$'s latent factor vector
- $f$ = number of latent factors (rank of the model)

## Objective Function

Regularised MF minimises the squared error over observed ratings:

$$\min_{P, Q} \sum_{(u,i) \in K} \left( r_{ui} - q_i^T p_u \right)^2 + \lambda \left( \|q_i\|^2 + \|p_u\|^2 \right)$$

where $K$ = set of observed (user, item) pairs and $\lambda$ = regularisation strength.

## Learning Algorithms

| Algorithm | Approach | Use Case |
|---|---|---|
| **SGD** (e.g. SVD) | Iteratively update all parameters in the direction opposite to the gradient | General purpose; efficient for large sparse data |
| **ALS** | Alternately fix $Q$ and solve for $P$, then fix $P$ and solve for $Q$ | Parallelisable; preferred when handling implicit feedback |

> [!example]- Prediction Example
> User A has preference vector $p_A = [0.9, 0.1]$ (loves action, dislikes drama).
> Movie X has factor vector $q_X = [0.8, 0.3]$.
> Predicted rating: $\hat{r} = 0.9 \times 0.8 + 0.1 \times 0.3 = 0.72 + 0.03 = 0.75$

> [!warning] Inner Product Limitation
> The inner product $q_i^T p_u$ cannot represent all user-item relationship patterns; it fails when the ranking order cannot be expressed as a dot product in low-dimensional space. Neural models like NCF address this by replacing the inner product with a learned interaction function.

## Significance

Matrix Factorization (popularised by the Netflix Prize, Koren et al. 2009) remains one of the most widely deployed recommendation algorithms due to its scalability, accuracy on explicit feedback, and elegant mathematical formulation.
