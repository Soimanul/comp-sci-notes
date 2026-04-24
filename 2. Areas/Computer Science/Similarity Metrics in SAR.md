**Tags:** #concept #reco
**Related:** [[Item-Item Similarity in SAR]], [[Co-occurrence Computation]], [[SAR Algorithm]]

## Definition

**Similarity metrics in SAR** are the normalisation functions applied to the raw co-occurrence matrix $C$ to produce the final item-item similarity matrix $S$. The choice of metric controls the accuracy vs. serendipity trade-off.

> [!info] Key Intuition
> Raw co-occurrence favours popular items. Normalisation adjusts for popularity so that less common co-occurrences can still reflect meaningful similarity.

## Metrics

Let $C_{ij}$ = co-occurrence count of items $i$ and $j$, and $C_{ii}$ = number of users who interacted with item $i$.

| Metric | Formula | Behaviour |
|---|---|---|
| **Count** | $S_{ij} = C_{ij}$ | No normalisation; popular items dominate |
| **Jaccard** | $S_{ij} = \dfrac{C_{ij}}{C_{ii} + C_{jj} - C_{ij}}$ | Balanced; penalises both high individual popularity |
| **Lift** | $S_{ij} = \dfrac{C_{ij} \cdot N}{C_{ii} \cdot C_{jj}}$ | Favours niche items; rewards disproportionate co-occurrence |
| **Mutual Information** | $S_{ij} = \log \dfrac{C_{ij} \cdot N}{C_{ii} \cdot C_{jj}}$ | Information-theoretic; biased toward low-frequency items |
| **Lexicographers MI** | $S_{ij} = C_{ij} \cdot \log \dfrac{C_{ij} \cdot N}{C_{ii} \cdot C_{jj}}$ | Corrects MI bias by multiplying by co-occurrence frequency |
| **Cosine** | $S_{ij} = \dfrac{C_{ij}}{\sqrt{C_{ii} \cdot C_{jj}}}$ | Angle between item column vectors; symmetric and bounded |
| **Inclusion Index** | $S_{ij} = \dfrac{C_{ij}}{\min(C_{ii}, C_{jj})}$ | Measures directional overlap; $S_{ij} = 1$ if one item's fans are a subset of the other's |

where $N$ = total number of users.

> [!example]- Count vs Lift Trade-off
> Item A: 10,000 interactions. Item B: 50 interactions. 30 users bought both.
> - **Count**: $S = 30$ → Item A (very popular) appears similar to almost everything
> - **Lift**: $S = 30 \times N / (10000 \times 50)$ → rewards the disproportionately strong co-occurrence between A and B despite B's low popularity

> [!warning] Default Recommendation
> Jaccard is the default balanced choice. Use Lift when long-tail discovery is the business goal. Avoid Count as a standalone metric in production — it returns popularity-biased recommendations.

## Significance

The metric is a tunable hyperparameter. Different datasets and business objectives call for different metrics — a diversity-focused streaming service might prefer Lift, while a reliability-focused e-commerce site might prefer Jaccard.
