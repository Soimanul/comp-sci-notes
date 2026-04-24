**Tags:** #concept #reco
**Related:** [[User Item Interaction Model]], [[User-Based Collaborative Filtering]], [[Item-Based Collaborative Filtering]], [[Matrix Factorization]], [[Cold Start Problem]]

## Definition

**Collaborative filtering** (CF) is a recommendation approach that predicts a user's preferences by discovering **patterns in the collective behaviour of many users** — without using any item or user attribute features.

> [!info] Key Intuition
> "Users who agreed in the past tend to agree again in the future." If Jeremy and Tao both loved Movie A and B, and Tao also loved Movie C, then Jeremy probably likes Movie C too. The wisdom of the crowd drives recommendations.

## Core Mechanism

CF operates on the **interaction matrix R** (users × items). The missing entries represent unknown preferences that the model must predict:

| | Item A | Item B | Item C | Item D |
|---|---|---|---|---|
| User A | 4 | ? | 5 | ? |
| User B | ? | 1 | ? | 5 |
| User C | ? | ? | 4 | 4 |

The `?` entries are what CF predicts by finding patterns in the observed data.

## Two Types

| Type | Approach |
|---|---|
| [[User-Based Collaborative Filtering]] | Find users similar to the target user; recommend what they liked |
| [[Item-Based Collaborative Filtering]] | Find items similar to what the target user liked; recommend those |

## Pros and Cons

| Pros | Cons |
|---|---|
| No item/user attribute features needed | Suffers from [[Cold Start Problem]] for new users/items |
| Discovers non-obvious cross-domain preferences | Requires significant interaction volume |
| Works for any item type | Scalability challenges at millions of users |
| Community wisdom drives serendipitous discovery | Popularity bias: popular items get recommended more |

> [!warning] Common Misconception
> Collaborative filtering does **not** understand item content. It treats items as opaque entities identified only by their interaction patterns. Two items could be very similar in content but CF would not know unless users who liked one also interacted with the other.

## Significance

Collaborative filtering is the most widely deployed recommendation approach in production. [[Matrix Factorization]] (SVD, ALS) is the dominant CF algorithm, and [[Neural Collaborative Filtering]] extends it to deep learning.
