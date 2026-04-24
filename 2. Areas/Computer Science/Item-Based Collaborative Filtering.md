**Tags:** #concept #reco
**Related:** [[Collaborative Filtering]], [[User-Based Collaborative Filtering]], [[SAR Algorithm]], [[Item-Item Similarity in SAR]]

## Definition

**Item-based collaborative filtering** generates recommendations by finding **items that are similar to items the target user has already liked**, based on co-interaction patterns across all users.

> [!info] Key Intuition
> "People who bought this also bought that." If many users who bought Item A also bought Item B, then A and B are similar. When a user likes A, recommend B. This is the principle behind Amazon's famous "Customers who bought X also bought Y" feature.

## Algorithm Steps

1. Compute an **item-item similarity matrix** from co-interaction patterns (cosine similarity, Jaccard, etc.).
2. For the target user, take items they've interacted with.
3. For each of those items, find the K most similar items.
4. Aggregate and rank candidate items, filtering out already-seen items.

## Pros and Cons

| Pros | Cons |
|---|---|
| More scalable than user-based: item catalogue changes slowly | Cold start for new items (no co-interaction history) |
| Item similarities are stable over time | Can create filter bubbles (always similar items) |
| Can be precomputed offline | Still requires significant interaction volume |
| No need for user feature data | |

> [!example]- Example
> On Amazon, if users who bought "Harry Potter" almost always also bought "The Hobbit", then item-based CF will recommend The Hobbit to any new user who just bought Harry Potter.

> [!warning] Common Misconception
> Item-based CF does NOT use item content (title, description, genre). Similarity is purely based on **who interacted with what** — two items are "similar" if the same users tended to interact with both, regardless of what the items actually are.

## Significance

Item-based CF is the foundation of the [[SAR Algorithm]] and is more practical than user-based CF for large-scale production systems because item-item similarities can be precomputed and cached efficiently.
