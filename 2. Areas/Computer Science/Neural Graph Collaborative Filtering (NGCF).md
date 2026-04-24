**Tags:** #concept #reco #dl
**Related:** [[Graph Neural Networks]], [[Message Passing in GNNs]], [[High-Order Connectivity in GNNs]], [[LightGCN]]

## Definition

**Neural Graph Collaborative Filtering (NGCF)** is a GNN-based recommendation model that explicitly encodes collaborative signals by propagating embeddings through the user-item interaction graph, capturing high-order connectivity for improved recommendations.

> [!info] Key Intuition
> NGCF says: the embedding of user $u$ should be informed not just by $u$'s own latent vector, but by the embeddings of items $u$ has interacted with, and by the embeddings of other users who interacted with those items. Each GNN layer propagates this collaborative signal one hop further.

## Architecture

**Embedding layer:** Initialise user embeddings $E_U \in \mathbb{R}^{M \times d}$ and item embeddings $E_I \in \mathbb{R}^{N \times d}$.

**Propagation layer** (for user $u$ at layer $l$):

$$e_u^{(l)} = \text{LeakyReLU}\left(W_1 e_u^{(l-1)} + \sum_{i \in \mathcal{N}_u} \frac{1}{\sqrt{|\mathcal{N}_u||\mathcal{N}_i|}} \left(W_1 e_i^{(l-1)} + W_2 (e_i^{(l-1)} \odot e_u^{(l-1)})\right)\right)$$

The $W_2 (e_i \odot e_u)$ term is an **interaction term** between the neighbour and the target node.

**Final embedding:** Concatenate embeddings from all $L$ layers:
$$e_u^* = e_u^{(0)} \| e_u^{(1)} \| \ldots \| e_u^{(L)}$$

**Prediction:** $\hat{r}_{ui} = (e_u^*)^T e_i^*$

## Loss

BPR pairwise loss over (user, positive item, negative item) triples.

## NGCF vs. LightGCN

| Feature | NGCF | LightGCN |
|---|---|---|
| Interaction term $W_2(e_i \odot e_u)$ | Yes | No |
| Feature transformation ($W_1$) | Yes | No |
| Non-linear activation | LeakyReLU | None |
| Complexity | Higher | Lower |
| Performance | Good | Better (less overfitting) |

> [!warning] Over-complexity
> LightGCN ablation studies showed that the non-linear transformation and interaction term in NGCF often hurt performance by adding unnecessary complexity. Simpler propagation achieves better results on most benchmarks.

## Significance

NGCF (Wang et al., 2019) was the first model to show that explicit graph structure propagation consistently outperforms MF on collaborative filtering benchmarks. It directly motivated LightGCN's simplification.
