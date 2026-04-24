**Tags:** #concept #reco
**Related:** [[SAR Algorithm]], [[Co-occurrence Computation]], [[Item-Item Similarity in SAR]], [[Time Decay]], [[Weighted Interaction Count]]

## Definition

The **affinity matrix** $A$ captures the strength of the relationship between every user and every item. It is the user-item score matrix that SAR uses as one of two inputs to compute recommendation scores.

> [!info] Key Intuition
> The affinity matrix answers "How much does user $u$ care about item $i$?" It can be built from explicit ratings or from weighted implicit interactions, with optional time decay so that recent behaviour counts more than old behaviour.

## Building the Affinity Matrix

### From Interaction Type

SAR accepts both explicit and implicit feedback:

| Input Type | How It Is Used |
|---|---|
| **Explicit** | Ratings (e.g. 1–5 stars) used directly as affinity values |
| **Implicit** | Interaction events (view, click, add-to-cart, purchase) each assigned a configurable weight (e.g. view=1, click=2, purchase=4) |

### From Interaction Timing (Temporal Discount)

A **time-decay factor** can be applied to give more importance to recent interactions:

$$A(u, i) = \sum_{\text{events}} w_e \cdot 2^{-\Delta t / T}$$

where:
- $w_e$ = event weight
- $\Delta t$ = time elapsed since the event
- $T$ = half-life parameter: events $T$ time units before $t_0$ receive half the weight of events at $t_0$

> [!example]- Effect of Half-Life Parameter T
> With $T = 30$ days:
> - A purchase made today contributes weight $4 \times 2^0 = 4$
> - The same purchase 30 days ago contributes $4 \times 2^{-1} = 2$
> - The same purchase 60 days ago contributes $4 \times 2^{-2} = 1$

> [!warning] Binarisation Before Co-occurrence
> For computing the item-item co-occurrence matrix, the affinity matrix is binarised (values → 0 or 1). The full continuous affinity values are only used in the final recommendation score step.

## Significance

The affinity matrix is a key input to the SAR recommendation score: $\text{rec}(u, k) = \sum_i A(u, i) \cdot S(k, i)$. The richer and more accurate the affinity signal, the better the final recommendations.
