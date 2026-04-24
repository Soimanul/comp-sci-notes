**Tags:** #concept #reco
**Related:** [[Offline vs Online Metrics]], [[Precision@K]], [[NDCG@K]], [[MAP@K]]

## Definition

**Recall@K** is a ranking metric that measures the **proportion of all relevant items that appear in the top-K recommendations**.

$$\text{Recall@K} = \frac{\text{Number of relevant items in top-K recommendations}}{\text{Total number of relevant items}}$$

> [!info] Key Intuition
> Recall@K answers: "Of all the items this user would have liked, what fraction did I manage to surface in my top K?" It measures how **complete** your coverage of the user's interests is.

## Example

| Total relevant items for user | 5 |
|---|---|
| Relevant items found in top 10 | 3 |
| **Recall@10** | **3/5 = 0.60** |

## Precision vs Recall Trade-off

Increasing K raises Recall (more items shown → more relevant items captured) but may lower Precision (diluted by irrelevant items). The K value is a business decision based on how many recommendations the UI can show.

> [!warning] Common Misconception
> High Recall@K doesn't mean the recommendations are good — you could get perfect recall by showing the **entire item catalogue**. Recall must be evaluated alongside Precision@K or [[NDCG@K]].

## Significance

Recall@K is critical when **missing a relevant item is costly** — for example, in medical recommendations (missing a relevant treatment) or job matching (missing a qualified candidate). In consumer apps like Netflix, Precision@K often matters more because screen real estate is limited.
