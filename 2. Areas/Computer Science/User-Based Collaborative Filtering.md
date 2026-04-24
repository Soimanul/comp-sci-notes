**Tags:** #concept #reco
**Related:** [[Collaborative Filtering]], [[Item-Based Collaborative Filtering]], [[SAR Algorithm]]

## Definition

**User-based collaborative filtering** generates recommendations by finding **users who are similar to the target user** and recommending items those similar users have liked but the target user has not yet seen.

> [!info] Key Intuition
> "Find your tribe, then steal their taste." If users B and C are very similar to user A (they've rated the same items similarly), then items B and C liked that A hasn't seen are strong candidates for A.

## Algorithm Steps

1. Compute a **user-user similarity matrix** using the interaction history (cosine similarity, Pearson correlation, etc.).
2. For the target user, find the **K most similar users** (nearest neighbours).
3. Collect items liked by those neighbours that the target user hasn't interacted with.
4. Score and rank those items, weighted by neighbour similarity.

## Pros and Cons

| Pros | Cons |
|---|---|
| Intuitive and interpretable | Does not scale well: O(U²) similarity computation for U users |
| Can surface serendipitous discoveries | User similarity is sparse and noisy when data is limited |
| Does not require item features | Cold start for new users — no history to find neighbours |

> [!example]- Example
> Users A and B both gave 5 stars to the same 10 obscure indie films. B also rated Film X highly. User-based CF recommends Film X to A because B is A's top neighbour.

> [!warning] Common Misconception
> User-based CF does not scale well to large user bases. For millions of users, computing and updating the full user-user similarity matrix is prohibitively expensive. **Item-based CF** and **matrix factorization** are preferred at scale.

## Significance

User-based CF is the original neighbourhood method and conceptually central to understanding collaborative filtering. In practice, [[Item-Based Collaborative Filtering]] is more commonly used in production due to its better scalability.
