**Tags:** #concept #reco
**Related:** [[Offline vs Online Metrics]], [[Precision@K]], [[Recall@K]], [[NDCG@K]]

## Definition

**MAP@K** (Mean Average Precision at K) evaluates the **average precision** for each user across the entire dataset, accounting for the position of relevant items in the ranking.

For a single user, Average Precision@K (AP@K):

$$\text{AP@K} = \frac{1}{\min(K, R)} \sum_{k=1}^{K} \text{Precision@k} \cdot \mathbf{1}[\text{item at rank } k \text{ is relevant}]$$

where $R$ is the total number of relevant items. MAP@K averages AP@K over all users.

> [!info] Key Intuition
> MAP@K rewards models that put relevant items **earlier** in the list. A relevant item at position 1 boosts the precision average much more than one at position K.

## Relationship to Other Metrics

| Metric | Cares about Position? | Graded Relevance? |
|---|---|---|
| [[Precision@K]] | No | No |
| [[Recall@K]] | No | No |
| MAP@K | Yes (via AP average) | No |
| [[NDCG@K]] | Yes (log discount) | Yes |

> [!example]- Example
> User has 3 relevant items. Recommended list: [✓, ✗, ✓, ✗, ✓]
> Precision at ranks: P@1=1, P@3=0.67, P@5=0.60
> AP@5 = (1 + 0.67 + 0.60) / 3 = **0.76**

## Significance

MAP@K is closely related to [[NDCG@K]] and is widely used in information retrieval and recommendation benchmarks. It provides a single-number summary of ranking quality across all users, making it useful for comparing models in research settings.
