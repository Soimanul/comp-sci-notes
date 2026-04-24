**Tags:** #hub #reco
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> A recommender system operates on three types of input data: explicit feedback (ratings, reviews), implicit feedback (clicks, views), and user/item features. Raw interaction data must be transformed before use — via counting, weighting, time-decay, binarization, or one-hot encoding. Negative samples are constructed artificially since implicit data only records positives.

## Overview

Before training any model, you must understand and pre-process your data. The data pipeline shapes what signal the model can learn from, and poor data design is the most common reason recommendation systems fail in practice.

## Knowledge Map

- [[User Item Interaction Model]]
- [[Explicit Feedback]]
- [[Implicit Feedback]]
- [[User and Item Features]]
- [[Knowledge-Based Recommendation Data]]
- [[Cold Start Problem]]
- [[Interaction Count]]
- [[Weighted Interaction Count]]
- [[Time Decay]]
- [[Weighted Time Decay]]
- [[One-Hot Encoding]]
- [[Binarization]]
- [[Negative Sampling in Recommenders]]
- [[Data Split Strategies]]

## Key Concepts

| Concept | One-line Summary |
|---|---|
| [[Explicit Feedback]] | Direct signals: ratings, reviews, surveys |
| [[Implicit Feedback]] | Indirect signals: clicks, views, purchases |
| [[Cold Start Problem]] | No data for new users or items |
| [[Interaction Count]] | Raw count of user-item interactions |
| [[Negative Sampling in Recommenders]] | Constructing artificial negative examples for training |

> [!question]- Exam Questions
> - What is the difference between explicit and implicit feedback? Give two pros and cons of each.
> - Why is implicit feedback only positive, and what does negative sampling solve?
> - Describe three data transformation techniques for building affinity scores.
> - What is the cold start problem and what types of data help mitigate it?
> - Explain the difference between random, stratified, and chronological data splits.
