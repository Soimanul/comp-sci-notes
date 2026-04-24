**Tags:** #concept #reco #dl
**Related:** [[Neural Graph Collaborative Filtering (NGCF)]], [[Graph Neural Networks]], [[Message Passing in GNNs]]

## Definition

**LightGCN** is a simplified GNN for collaborative filtering that removes the feature transformation matrix and non-linear activation from NGCF, retaining only the **normalised neighbourhood aggregation** and **layer combination** — and achieving better performance with fewer parameters.

> [!info] Key Intuition
> NGCF's ablation studies showed that the transformation matrices and non-linear activations consistently hurt performance. LightGCN removes them entirely: user/item embeddings are propagated as-is through the graph, and the final representation is a weighted sum across all layers.

## Architecture

**Layer propagation (no parameters):**
$$e_u^{(l)} = \sum_{i \in \mathcal{N}_u} \frac{1}{\sqrt{|\mathcal{N}_u| |\mathcal{N}_i|}} e_i^{(l-1)}$$

$$e_i^{(l)} = \sum_{u \in \mathcal{N}_i} \frac{1}{\sqrt{|\mathcal{N}_i| |\mathcal{N}_u|}} e_u^{(l-1)}$$

**Final representation** (weighted combination of all layers):
$$e_u^* = \sum_{l=0}^{L} \alpha_l e_u^{(l)}, \quad \alpha_l = \frac{1}{L+1} \text{ (uniform by default)}$$

**Prediction:** $\hat{r}_{ui} = (e_u^*)^T e_i^*$

## Only Learnable Parameters

The **initial embeddings** $e_u^{(0)}$ and $e_i^{(0)}$ are the only trainable parameters. Propagation is parameter-free.

## Matrix Form

In matrix form, one step of LightGCN propagation is:

$$E^{(l)} = \tilde{A} E^{(l-1)}, \quad \tilde{A} = D^{-1/2} A D^{-1/2}$$

where $A$ is the user-item adjacency matrix and $D$ is the degree matrix.

## Comparison

| Feature | NGCF | LightGCN |
|---|---|---|
| Transformation matrices | Yes ($W_1, W_2$) | None |
| Non-linearity | LeakyReLU | None |
| Layer combination | Concatenation | Weighted sum |
| Trainable params | More | Fewer |
| Performance | Good | Better |

> [!example]- Why Does Simpler Work Better?
> In CF, all features come from ID embeddings (not content features), so there is no benefit from linear projection. The normalised propagation effectively implements a smooth graph convolution that spreads collaborative signals across the graph.

## Significance

LightGCN (He et al., 2020) is the standard GNN baseline for collaborative filtering, showing that "less is more" in graph-based CF. It is widely used in production recommendation systems.
