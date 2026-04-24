**Tags:** #concept #reco
**Related:** [[Matrix Factorization]], [[SVD for Recommendations]], [[ALS Algorithm]], [[Inner Product Limitation]]

## Definition

**Latent factors** are the hidden, low-dimensional representations learned by matrix factorization to characterise both users and items. A user factor vector $p_u \in \mathbb{R}^f$ encodes that user's preferences; an item factor vector $q_i \in \mathbb{R}^f$ encodes that item's properties.

> [!info] Key Intuition
> Latent factors compress the high-dimensional user-item matrix into a small number of dimensions $f$. The dimensions may correspond to interpretable concepts (comedy vs. drama, budget vs. luxury) or be uninterpretable — but either way, users and items that share similar factor values will produce high predicted ratings when their vectors are multiplied.

## Structure

Given $m$ users, $n$ items, and $f$ latent dimensions:
- **Item factor matrix** $Q \in \mathbb{R}^{n \times f}$: each row $q_i$ is the latent vector for item $i$
- **User factor matrix** $P \in \mathbb{R}^{m \times f}$: each row $p_u$ is the latent vector for user $u$
- **Predicted rating**: $\hat{r}_{ui} = q_i^T p_u$

The rank $f$ (number of latent factors) is a hyperparameter controlling model capacity.

> [!example]- Interpretation
> For a movie dataset, one latent dimension might separate "serious art films" (high) from "light comedies" (low). An item's factor value on this dimension captures how serious it is; a user's factor value captures how much they prefer serious films.
> 
> Most dimensions won't be this cleanly interpretable — they emerge from the data without labels.

> [!warning] Interpretability vs. Accuracy
> More factors $f$ → higher capacity → lower training error, but risk of overfitting. The optimal $f$ is found via cross-validation. Regularisation $\lambda$ controls overfitting alongside $f$.

## Significance

Latent factors are the central innovation of model-based collaborative filtering. By learning a compact shared representation, matrix factorization can predict ratings for user-item pairs with no observed interactions, directly addressing the sparsity problem of memory-based methods like SAR.
