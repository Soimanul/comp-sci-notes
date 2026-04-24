**Tags:** #concept #reco
**Related:** [[SAR Algorithm]], [[Co-occurrence Computation]]

## Definition

**Item-item similarity in SAR** is the pairwise similarity score between any two items, computed from co-interaction patterns in the user-item matrix. It forms the item-item similarity matrix $S$.

> [!info] Key Intuition
> Items are similar if the same users tend to interact with both. The similarity metric controls the trade-off between recommending popular items (Count) vs. surprising items (Lift) vs. a balance (Jaccard).

## Similarity Metrics

| Metric | Behaviour |
|---|---|
| **Count** | Favours predictability — popular items are recommended most |
| **Lift** | Favours discoverability and serendipity — niche items with a loyal user base are highlighted |
| **Jaccard** | A compromise between Count and Lift |
| **Mutual Information** | Measures information explained by the co-occurrence of two items |
| **Lexicographers Mutual Information** | Corrects MI bias for low-frequency items by multiplying by co-occurrence frequency |
| **Cosine Similarity** | Interpreted as the angle between column vectors in the user-item matrix |
| **Inclusion Index** | Measures the overlap between items |

> [!example]- Count vs Lift Trade-off
> Item A (sold 10,000 times) and Item B (sold 50 times). 30 users bought both.
> - **Count**: similarity = 30 (favours A, a popular item).
> - **Lift**: similarity = 30 / (10,000 × 50) × total users (favours B because co-occurrence is disproportionately high given its low popularity → serendipitous find).

## Significance

The choice of similarity metric directly affects the diversity vs. accuracy trade-off of SAR recommendations. Jaccard is the default balanced choice; Lift is preferred when discovering niche or long-tail items is the business goal.
