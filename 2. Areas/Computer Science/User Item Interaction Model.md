**Tags:** #concept #reco
**Related:** [[Recommendation System Overview]], [[Explicit Feedback]], [[Implicit Feedback]], [[User and Item Features]]

## Definition

The **user-item interaction model** is the foundational data structure of a recommendation system. Every recommender operates on three components:

- **User** — the entity receiving recommendations (a customer, viewer, player).
- **Item** — the entity being recommended (a product, video, song, restaurant).
- **Interaction (Feedback)** — a record of engagement between a user and an item (purchase, click, rating, view time).

> [!info] Key Intuition
> Everything in recommendation reduces to: *"Given what user U has done with items in the past, what item should we surface next?"* The interaction record is the bridge between user and item.

## The Interaction Matrix R

Interactions are collected into a matrix where rows are users and columns are items:

$$R_{ui} = \text{feedback of user } u \text{ on item } i$$

This matrix is typically **extremely sparse**: users interact with only a tiny fraction of available items. The job of the recommendation model is to fill in the missing values.

> [!example]- Example Matrix
> | | Movie A | Movie B | Movie C | Movie D |
> |---|---|---|---|---|
> | User 1 | 4 | ? | 5 | ? |
> | User 2 | ? | 1 | ? | 5 |
> | User 3 | ? | ? | 4 | 4 |
>
> The `?` entries are what the recommender must predict.

## Types of Interaction Data

| Type | Examples |
|---|---|
| [[Explicit Feedback]] | 1–5 star ratings, survey results, text reviews |
| [[Implicit Feedback]] | Clicks, purchases, view time, impressions |
| [[User and Item Features]] | Demographics, product attributes |
| [[Knowledge-Based Recommendation Data]] | User requirements, goals, constraints |

## Significance

The user-item interaction model is the starting point for all recommendation algorithms. The choice of how to record and weight interactions directly determines what the model can learn.
