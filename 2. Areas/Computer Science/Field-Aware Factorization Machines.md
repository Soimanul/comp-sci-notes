**Tags:** #concept #reco
**Related:** [[Factorization Machines]], [[Inner Product Limitation]]

## Definition

**Field-Aware Factorization Machines (FFM)** extend FM by assigning each feature a separate latent vector for every **field** it interacts with, rather than a single shared latent vector.

> [!info] Key Intuition
> In FM, the interaction between "user=Alice" and "item=Movie42" uses the same latent vector for Alice as the interaction between "user=Alice" and "device=Mobile". FFM says these are different relationships — Alice behaves differently when interacting with items vs. with contexts — so she should have separate vectors per field.

## Fields

A **field** is a group of features that represent the same semantic category:
- Field 1: User ID features
- Field 2: Item ID features
- Field 3: Contextual features (time, device, location)

Each feature $i$ belonging to field $f_j$ has a separate latent vector $v_{i, f_j}$ for interactions with features in field $f_j$.

## Model

$$\hat{y}(x) = w_0 + \sum_{i} w_i x_i + \sum_{i=1}^{n} \sum_{j=i+1}^{n} \langle v_{i, f_j}, v_{j, f_i} \rangle \, x_i x_j$$

Where $v_{i, f_j}$ is the latent vector for feature $i$ when interacting with features in field $f_j$.

## Complexity

FFM requires $O(nfk)$ parameters (vs. $O(nk)$ for FM), where $f$ = number of fields. Computation is $O(kn^2)$ — the linear trick of FM no longer applies, so FFM is more expensive.

> [!warning] Trade-off
> FFM achieves better accuracy on datasets with strong field-specific interaction patterns, but requires significantly more memory and compute. In practice, FM is often preferred for large-scale online serving; FFM is used when accuracy is critical and the field structure is well-defined.

## Comparison

| Property | FM | FFM |
|---|---|---|
| Latent vectors per feature | 1 | $f$ (one per field) |
| Parameters | $O(nk)$ | $O(nfk)$ |
| Computation | $O(kn)$ | $O(kn^2)$ |
| Accuracy | Good | Better (with clear field structure) |

## Significance

FFM won multiple CTR prediction competitions (Criteo, Avazu) when first published. It established that field-awareness is a useful inductive bias for ad recommendation, and the idea influenced later architectures like DeepFM.
