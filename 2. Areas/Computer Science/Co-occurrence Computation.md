**Tags:** #concept #reco
**Related:** [[SAR Algorithm]], [[Affinity Matrix]], [[Item-Item Similarity in SAR]]

## Definition

**Co-occurrence computation** is the process of computing how often two items appear together in the same user's interaction history. It produces the co-occurrence matrix $C$, which is then normalised into the item-item similarity matrix $S$.

> [!info] Key Intuition
> If many users have interacted with both Item A and Item B, those items have high co-occurrence. Co-occurrence is the raw count signal; the chosen similarity metric then normalises it.

## Algorithm

Given:
- $U'$ = binarised affinity matrix (1 if user has interacted with item, 0 otherwise), shape = (users × items)

The co-occurrence matrix is:

$$C = U'^T \cdot U'$$

Shape: (items × items). Entry $C_{ij}$ = number of users who interacted with both item $i$ and item $j$.

> [!example]- Worked Computation
> ```
> U' (binarised affinity):       C = U'^T * U':
>  Item: 1 2 3 4                  Item: 1 2 3 4
> User1: 1 0 0 1                  Item1: 1 0 1 0
> User2: 0 1 0 0               →  Item2: 0 1 1 0
> User3: 1 0 1 0                  Item3: 1 1 2 1
> User4: 0 1 1 0                  Item4: 0 0 1 1
> ```
> $C_{33} = 2$ because Users 3 and 4 both interacted with Item 3.
> The diagonal $C_{ii}$ = total users who interacted with item $i$.

## From Co-occurrence to Similarity

The co-occurrence matrix $C$ is normalised into a similarity matrix $S$ using the chosen [[Similarity Metrics in SAR|similarity metric]] (Jaccard, Lift, Cosine, etc.):

$$S = \text{normalise}(C)$$

> [!warning] Diagonal Handling
> The diagonal of $C$ (self-co-occurrence) must be handled carefully. Most similarity metrics either ignore it or treat it as the total interaction count per item.

## Significance

Co-occurrence is what makes SAR a purely transactional algorithm — it only requires user-item interaction logs and no item content features. The co-occurrence matrix can be updated incrementally as new interactions arrive.
