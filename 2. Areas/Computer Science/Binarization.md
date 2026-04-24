**Tags:** #concept #reco
**Related:** [[Interaction Count]], [[One-Hot Encoding]], [[Implicit Feedback]]

## Definition

**Binarization** is a data transformation that converts **numerical values into binary (0/1) indicators** based on a threshold. In recommendation systems, it is used to convert raw interaction scores or ratings into simple positive/negative labels.

$$b_{ui} = \begin{cases} 1 & \text{if } r_{ui} \geq \theta \\ 0 & \text{otherwise} \end{cases}$$

where $\theta$ is the binarization threshold.

> [!info] Key Intuition
> Binarization simplifies the prediction task. Instead of predicting the exact rating value (regression), the model predicts a binary preference: "did the user like this or not?" This is especially useful when the distinction between exact values doesn't matter for ranking.

## When to Use

- When converting ratings to like/dislike for implicit-feedback models.
- When reducing noise in interaction data (very low counts treated as no interaction).
- As a preprocessing step for models that require binary input.

> [!example]- Example
> Movie ratings on a 1–5 scale: ratings ≥ 4 → 1 (positive), ratings < 4 → 0 (negative).
> Interaction counts: count ≥ 1 → 1 (interacted), 0 → 0 (not interacted). This is the standard binarization for implicit feedback.

> [!warning] Common Misconception
> Binarization loses information about the intensity of preference. A user who watched a movie 10 times and a user who watched it once both become 1. For ranking-sensitive applications, [[Weighted Interaction Count]] or [[Weighted Time Decay]] preserve more signal.

## Significance

Binarization is a practical simplification that makes recommendation models more tractable and is the standard transformation for implicit feedback data used in models like [[Bayesian Personalized Ranking]].
