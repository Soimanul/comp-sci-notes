**Tags:** #hub #reco
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> The two main paradigms for recommendation are collaborative filtering (learn from the community of users) and content-based filtering (learn from item and user attributes). Collaborative filtering requires no feature engineering but struggles with cold start. Content-based filtering handles cold start but may overspecialise.

## Overview

The choice of filtering approach is the most fundamental architectural decision in building a recommendation system. In practice, most production systems combine both in a **hybrid** approach.

## Knowledge Map

- [[Collaborative Filtering]]
- [[Content-Based Filtering]]
- [[User-Based Collaborative Filtering]]
- [[Item-Based Collaborative Filtering]]

## Key Concepts

| Concept | Key Question |
|---|---|
| [[Collaborative Filtering]] | What did similar users like? |
| [[Content-Based Filtering]] | What attributes make items relevant to this user? |
| [[User-Based Collaborative Filtering]] | Find similar users, recommend what they liked |
| [[Item-Based Collaborative Filtering]] | Find similar items to what user has already liked |

> [!question]- Exam Questions
> - What is the core intuition of collaborative filtering?
> - How does content-based filtering address the cold start problem that collaborative filtering cannot?
> - What is the difference between user-based and item-based collaborative filtering?
> - Name one advantage and one disadvantage of each approach.
