**Tags:** #concept #reco
**Related:** [[Offline vs Online Metrics]], [[Precision@K]], [[Recall@K]], [[MAP@K]]

## Definition

**NDCG@K** (Normalised Discounted Cumulative Gain at K) is a ranking metric that evaluates both **whether** relevant items are recommended and **where** they appear in the ranking. Items higher up in the list contribute more to the score.

$$\text{NDCG@K} = \frac{\text{DCG@K}}{\text{IDCG@K}}$$

where DCG (Discounted Cumulative Gain) rewards relevant items at higher positions with a logarithmic discount:

$$\text{DCG@K} = \sum_{k=1}^{K} \frac{\text{rel}_k}{\log_2(k+1)}$$

and IDCG is the maximum possible DCG (the ideal ranking), used for normalisation.

> [!info] Key Intuition
> NDCG@K embodies the assumption that users click on the first recommendation far more than the last. A relevant item at position 1 is much more valuable than one at position 10.

## Worked Example

| Rank k | Item | Relevant? | rel_k | $\log_2(k+1)$ | DCG contribution |
|---|---|---|---|---|---|
| 1 | A | ✓ | 1 | 1.00 | 1.00 |
| 2 | B | ✗ | 0 | 1.58 | 0.00 |
| 3 | C | ✓ | 1 | 2.00 | 0.50 |

DCG@3 = 1.00 + 0 + 0.50 = **1.50**. If the ideal DCG@3 (both items at ranks 1 and 2) = 1.00 + 0.63 = 1.63, then NDCG@3 = 1.50/1.63 ≈ **0.92**

> [!warning] Common Misconception
> NDCG uses a **graded** relevance model: it can handle binary (0/1) or continuous relevance scores. The key insight is that NDCG ≠ Precision@K — two lists with the same Precision@K can have very different NDCG@K if the relevant items are in different positions.

## NDCG vs MAP

Both NDCG and [[MAP@K]] are position-sensitive. NDCG uses a logarithmic discount while MAP uses the rank position directly. NDCG is typically preferred for its smoother handling of graded relevance.

## Significance

NDCG@K is the most commonly used single metric for ranking quality in recommendation system benchmarks. It directly reflects the user experience by rewarding good recommendations at the top of the list.
