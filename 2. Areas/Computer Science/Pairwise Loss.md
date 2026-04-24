**Tags:** #concept #reco
**Related:** [[Pointwise Loss]], [[Bayesian Personalized Ranking]], [[NDCG@K]]

## Definition

**Pairwise loss** trains a model to correctly rank pairs of items by optimising that the score of a preferred item exceeds the score of a less preferred item by a margin. The model directly learns relative ordering rather than absolute scores.

> [!info] Key Intuition
> Instead of asking "what is the absolute rating of item A?", pairwise learning asks "should item A rank above item B for this user?". This is more aligned with how recommendation quality is actually measured.

## Pairwise Objective

Given user $u$, positive item $i$ (user interacted with), negative item $j$ (user did not interact with):

$$L = \sum_{(u, i, j)} \ell(\hat{r}_{ui} - \hat{r}_{uj})$$

Common choices for $\ell$:

| Loss function | Formula | Notes |
|---|---|---|
| Hinge loss | $\max(0, 1 - (\hat{r}_{ui} - \hat{r}_{uj}))$ | Hard margin |
| Logistic (BPR) | $-\log \sigma(\hat{r}_{ui} - \hat{r}_{uj})$ | Soft probabilistic |
| RankNet | Cross-entropy on predicted pairwise probabilities | Used in web search |

## Sampling

Pairwise methods require (user, positive, negative) triples. Negative sampling strategy matters:
- **Uniform**: sample any unobserved item as negative
- **Popularity-based**: sample popular items as hard negatives
- **Adaptive**: sample negatives close to the decision boundary

## Advantages Over Pointwise

| Property | Pointwise | Pairwise |
|---|---|---|
| Optimises | Absolute scores | Relative ordering |
| Label type needed | Explicit rating or click label | Just preference direction |
| Handles implicit feedback | Requires careful negatives | Natural formulation |
| Aligns with ranking metrics | Poor | Better |

> [!warning] Scalability
> The number of pairs grows quadratically in items. Efficient sampling is essential — only a small fraction of all pairs is used per epoch.

## Significance

Pairwise learning is the foundation of [[Bayesian Personalized Ranking]], which is the most widely used learning-to-rank method for implicit feedback recommendation.
