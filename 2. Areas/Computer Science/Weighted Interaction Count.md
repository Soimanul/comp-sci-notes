**Tags:** #concept #reco
**Related:** [[Interaction Count]], [[Time Decay]], [[Weighted Time Decay]], [[Affinity Matrix]]

## Definition

**Weighted interaction count** is a data transformation that extends [[Interaction Count]] by assigning different **weights** to different interaction types, reflecting their relative importance as preference signals.

$$\text{affinity}(u, i) = \sum_{t} w_{e_t} \cdot \mathbf{1}[\text{user } u \text{ interacted with item } i \text{ at time } t]$$

where $w_{e_t}$ is the weight for event type $e_t$.

> [!info] Key Intuition
> Not all interactions are equal. A purchase is a much stronger preference signal than a click or an impression. Assigning weights lets the affinity score reflect this: purchasing an item might have weight 5, clicking weight 1, and just viewing weight 0.1.

## Example Weight Scheme

| Interaction Type | Weight |
|---|---|
| Purchase | 5 |
| Add to cart | 3 |
| Click | 1 |
| Impression / View | 0.1 |

> [!example]- Example
> User 1 clicked Movie A twice (weight=1 each) and purchased Movie B once (weight=5).
> Weighted affinity: A → 2×1 = 2, B → 1×5 = 5. The model correctly prioritizes B.

## Significance

Weighted counting is a low-cost improvement over raw counting that significantly improves recommendation quality by reflecting the actual strength of user preference signals.
