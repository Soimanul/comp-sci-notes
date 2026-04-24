**Tags:** #concept #reco
**Related:** [[Weighted Interaction Count]], [[Time Decay]], [[Affinity Matrix]]

## Definition

**Weighted time decay** combines [[Weighted Interaction Count]] and [[Time Decay]] into a single affinity transformation: interactions are weighted by both their **type** (purchase vs click) and their **recency** (how long ago they occurred).

$$\text{affinity}(u, i) = \sum_{t} w_{e_t} \cdot \exp\!\left(-\frac{t_0 - t}{T}\right)$$

> [!info] Key Intuition
> This is the most realistic affinity score: a recent purchase contributes a high score, an old click contributes almost nothing. It captures both what the user did *and* when they did it.

## Parameters

| Parameter | Role |
|---|---|
| $w_{e_t}$ | Weight for interaction type $e_t$ (e.g., purchase=5, click=1) |
| $T$ | Half-life: interactions $T$ time units old get half the weight |
| $t_0 - t$ | Age of the interaction |

> [!example]- Example
> User 1 purchased Movie A 1 week ago (weight=5, decay≈0.9) and clicked Movie B 2 years ago (weight=1, decay≈0.02).
> Weighted time-decay affinity: A → 5×0.9 = 4.5, B → 1×0.02 = 0.02. The model strongly prioritises the recent purchase.

## Significance

Weighted time decay is the standard affinity transformation in production systems like [[SAR Algorithm]], capturing both the quality and freshness of user-item interactions.
