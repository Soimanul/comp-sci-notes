**Tags:** #concept #reco
**Related:** [[Implicit Feedback]], [[Pointwise Loss]], [[Pairwise Loss]], [[Bayesian Personalized Ranking]]

## Definition

**Negative sampling in recommenders** is the process of **artificially constructing negative training examples** for recommendation models, because implicit feedback only records positive interactions (items a user engaged with) and never explicitly records negative ones (items a user disliked or ignored).

> [!info] Key Intuition
> If you only train on positives, the model has no signal to distinguish good recommendations from bad ones — it just learns to predict "1" for everything. Negative sampling creates the contrast the model needs to learn a useful ranking function.

## The Problem

Implicit data is **only positive**:
- Observed: user clicked item → positive signal.
- Unobserved: user did NOT click item → **ambiguous** — could mean they disliked it, or simply never saw it.

## Sampling Strategies

| Strategy | Description |
|---|---|
| **Uniform random sampling** | Randomly sample unobserved (user, item) pairs as negatives |
| **Popularity-based sampling** | Sample negatives proportional to item popularity (harder negatives) |
| **Hard negative mining** | Select items the model scores high but are actually negative (most informative) |

## Key Tension

> [!warning] Common Misconception
> An unobserved item is **not necessarily a true negative**. The user may simply not have been exposed to it. This means negative samples are *noisy labels* — the model must learn to be robust to this ambiguity. This is one of the core motivations for [[Pairwise Loss]] and [[Bayesian Personalized Ranking]], which frame the problem as ranking observed above unobserved rather than predicting binary labels.

> [!example]- Example
> User U has purchased items {A, B, C}. The full item catalogue has {A, B, C, D, E, F, G, H}.
> Negative samples: randomly select 4 items from {D, E, F, G, H} → training labels: (U, D) = 0, (U, E) = 0, (U, F) = 0, (U, G) = 0.

## Significance

Negative sampling is a required preprocessing step for training most recommendation models on implicit feedback. The quality of negative sampling directly affects model performance, particularly for ranking objectives.
