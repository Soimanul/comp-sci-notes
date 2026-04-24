**Tags:** #concept #reco
**Related:** [[Graph Neural Networks]], [[Message Passing in GNNs]], [[Neural Graph Collaborative Filtering (NGCF)]], [[LightGCN]]

## Definition

**High-order connectivity** in GNNs for recommendation refers to the indirect relationships between users and items that exist through multi-hop paths in the user-item interaction graph — i.e., users connected not by direct interaction but through shared items (or items connected through shared users).

> [!info] Key Intuition
> First-order: User A and Item X are directly connected (A interacted with X).
> Second-order: User A → Item X → User B (A and B both interacted with X — similarity signal).
> Third-order: User A → Item X → User B → Item Y (Y is relevant to A because B, who is similar to A, liked Y).

## Multi-Hop Paths as Signals

| Order | Path | Signal |
|---|---|---|
| 1st | $u \to i$ | Direct preference |
| 2nd | $u \to i \to u'$ | User–user similarity |
| 2nd | $i \to u \to i'$ | Item–item similarity |
| 3rd | $u \to i \to u' \to i'$ | Indirect recommendation |
| $l$th | $\ldots$ | Increasingly abstract similarity |

## How GNNs Capture This

Each GNN layer propagates information one hop further. A $k$-layer GNN captures up to $k$-th order connectivity:
- Layer 1 aggregates direct neighbours (1st order)
- Layer 2 aggregates neighbours' neighbours (2nd order)
- Layer $k$ aggregates $k$-hop neighbourhood

## Why Standard CF Misses This

Matrix factorization optimises $R \approx PQ^T$ using only observed (user, item) pairs — it never explicitly models the indirect paths. The collaborative signal flows only through the shared latent space, not through explicit graph structure.

> [!example]- 3rd-Order Path
> User Alice bought "Deep Learning" (Item A). Bob also bought "Deep Learning" and "Python ML" (Item B). Item B was also bought by Carol.
> 3rd-order path: Alice → Item A → Bob → Item B — suggests Alice might like Item B.
> A 2-layer GNN on the bipartite graph will propagate this signal into Alice's representation.

## Significance

Capturing high-order connectivity is the key advantage of GNN-based recommendation over MF. It provides explicit collaborative signal propagation that improves recommendations especially for users with sparse interaction history.
