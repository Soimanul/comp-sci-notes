**Tags:** #concept #reco
**Related:** [[Offline vs Online Metrics]], [[Recall@K]], [[NDCG@K]], [[MAP@K]]

## Definition

**Precision@K** is a ranking metric that measures the **proportion of recommended items (top K) that are relevant** to the user.

$$\text{Precision@K} = \frac{\text{Number of relevant items in top-K recommendations}}{K}$$

> [!info] Key Intuition
> Precision@K answers: "Of the K items I showed this user, how many did they actually care about?" If you show 10 recommendations and 3 are relevant, Precision@10 = 0.30.

## Example

| Rank | Item | Relevant? |
|---|---|---|
| 1 | Movie A | ✓ |
| 2 | Movie B | ✗ |
| 3 | Movie C | ✓ |
| 4 | Movie D | ✗ |
| 5 | Movie E | ✗ |

Precision@5 = 2/5 = **0.40**

> [!warning] Common Misconception
> Precision@K does **not** care about the **order** of relevant items within the top K. Recommending the 2 relevant items at positions 4 and 5 vs positions 1 and 2 gives the same Precision@K but the former is clearly a worse ranker. Use [[NDCG@K]] or [[MAP@K]] when rank order matters.

## Precision@K vs Recall@K

| | Precision@K | [[Recall@K]] |
|---|---|---|
| Question answered | Of what I showed, how many were good? | Of all relevant items, how many did I find? |
| Penalises | Irrelevant recommendations | Missing relevant items |

## Significance

Precision@K is one of the most common evaluation metrics for top-K recommendation tasks. It directly models the user experience: a higher value means more of the shown recommendations are relevant.
