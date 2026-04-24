**Tags:** #concept #reco
**Related:** [[Matrix Factorization]], [[Latent Factors]], [[SVD for Recommendations]]

## Definition

**Alternating Least Squares (ALS)** is an optimisation algorithm for matrix factorization that alternates between fixing the item factors $Q$ and solving for user factors $P$ in closed form, then fixing $P$ and solving for $Q$.

> [!info] Key Intuition
> The MF objective is non-convex in $P$ and $Q$ jointly, but it becomes convex (and has a closed-form solution) when one is held fixed. ALS exploits this by turning one hard problem into a sequence of easy problems.

## Algorithm

**Repeat until convergence:**
1. Fix $Q$; solve for each $p_u$ independently: $p_u = (Q^T Q + \lambda I)^{-1} Q^T r_u$
2. Fix $P$; solve for each $q_i$ independently: $q_i = (P^T P + \lambda I)^{-1} P^T r_i$

Each step is an ordinary ridge regression problem with a closed-form solution.

## Implicit Feedback Extension

For implicit feedback (where $r_{ui}$ is a confidence value, not a direct rating):

$$\min_{P,Q} \sum_{u,i} c_{ui} (p_{ui} - q_i^T p_u)^2 + \lambda(\|P\|^2 + \|Q\|^2)$$

where:
- $p_{ui} \in \{0,1\}$ = binarised preference (1 if interacted)
- $c_{ui} = 1 + \alpha \cdot r_{ui}$ = confidence weight ($\alpha$ is a hyperparameter)

> [!example]- Why ALS Over SGD for Distributed Systems
> Each $p_u$ can be solved independently given $Q$, and each $q_i$ independently given $P$. This parallelises perfectly across machines — Spark's MLlib uses ALS for this reason.

> [!warning] Memory vs. SGD
> ALS stores the full factor matrices in memory during each step and requires matrix inversions of size $f \times f$. For very large $f$ this becomes expensive. SGD (SVD) is more memory-efficient but harder to parallelise.

## Comparison with SGD (SVD)

| Property | ALS | SGD (SVD) |
|---|---|---|
| Update type | Closed-form per user/item | Stochastic gradient step |
| Parallelism | Trivially parallel | Harder to parallelise |
| Implicit feedback | Natural extension | Requires modification |
| Convergence | Monotone decrease | Can oscillate; needs tuning |

## Significance

ALS is the standard algorithm for large-scale matrix factorization in distributed settings (Spark MLlib, implicit library in Python). Its native handling of implicit feedback makes it the default for e-commerce and streaming recommendation systems.
