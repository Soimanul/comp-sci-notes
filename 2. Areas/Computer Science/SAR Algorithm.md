**Tags:** #concept #reco
**Related:** [[Item-Based Collaborative Filtering]], [[Affinity Matrix]], [[Item-Item Similarity in SAR]], [[Co-occurrence Computation]]

## Definition

**SAR (Smart Adaptive Recommendations)** is a memory-based, item-item collaborative filtering algorithm that generates recommendations by combining a **user-item affinity matrix** with an **item-item similarity matrix**.

> [!info] Key Intuition
> SAR scores a recommendation by asking: "For every item this user has interacted with, how similar is the candidate item? Multiply affinity by similarity and sum." The more the user liked items that are similar to the candidate, the higher the recommendation score.

## Algorithm

Given:
- $A(u, i)$ = affinity score for user $u$ and item $i$ (based on [[Affinity Matrix]])
- $S(i, j)$ = similarity score between items $i$ and $j$ (based on [[Item-Item Similarity in SAR]])

The recommendation score for user $u$ for candidate item $k$ is:

$$\text{rec}(u, k) = \sum_{i \in \text{items}} A(u, i) \cdot S(k, i)$$

> [!example]- Worked Example
> User 1 has affinities: A(u,1)=5, A(u,2)=3, A(u,3)=2.5, A(u,4)=0, A(u,5)=0.
> Similarities to Item 4: S(4,1)=3, S(4,2)=2, S(4,3)=3, S(4,4)=4, S(4,5)=2.
> rec(User 1, Item 4) = 5×3 + 3×2 + 2.5×3 + 0×4 + 0×2 = 15 + 6 + 7.5 = **28.5**

## Pipeline

```
Transaction Data → Item-Item Similarity Matrix
                  ↓
           Affinity Matrix
                  ↓
            Dot Product
                  ↓
        Top-K Recommendations
```

Options: (1) remove already-seen items from recommendations; (2) apply temporal discount to affinity.

## Significance

SAR is a production-grade, highly interpretable recommendation algorithm. It is available as both a CPU and PySpark implementation in the Microsoft `recommenders` library, capable of handling millions of interactions efficiently.
