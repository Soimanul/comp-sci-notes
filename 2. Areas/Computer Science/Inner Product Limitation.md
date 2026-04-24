**Tags:** #concept #reco
**Related:** [[Matrix Factorization]], [[Latent Factors]], [[Factorization Machines]]

## Definition

The **inner product limitation** in Matrix Factorization refers to the failure of the dot product $q_i^T p_u$ to faithfully model all ranking relationships when the number of latent dimensions $f$ is small.

> [!info] Key Intuition
> The inner product forces all user-item affinities to be expressible as similarities in a single low-dimensional Euclidean space. When the true interaction structure cannot be embedded in that space, the model must make systematic ranking errors.

## The Problem

Consider four users: $u_1, u_2, u_3, u_4$ with observed cosine similarities in the interaction space:

$$s_{12} > s_{13} > s_{23} > s_{14} > s_{24} > s_{34}$$

In 2D Euclidean space it is geometrically impossible to place four points that satisfy all six pairwise similarity constraints simultaneously. Any 2D placement must violate at least one ordering.

> [!example]- Concrete Failure Case
> Suppose $u_1$ and $u_2$ are most similar, then $u_1$-$u_3$, etc.
> Placing $p_{u_1}$ to satisfy $s_{12}$ and $s_{13}$ forces $p_{u_3}$ close to $p_{u_2}$.
> But $s_{23}$ is meant to be small — contradiction. The model misranks items for these users.

## Consequence

When we cannot increase $f$ indefinitely (due to overfitting or memory), the inner product must approximate rather than exactly represent the true affinities. This introduces systematic errors in the ranking.

## Solution

[[Factorization Machines]] and [[Neural Collaborative Filtering]] replace or augment the inner product with a richer interaction function, eliminating this geometric constraint.

## Significance

Understanding this limitation motivates moving beyond MF: it explains why deep learning models consistently outperform pure MF on large, dense datasets where the interaction structure is complex.
