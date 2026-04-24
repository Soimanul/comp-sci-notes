**Tags:** #concept #dl
**Related:** [[Message Passing in GNNs]], [[High-Order Connectivity in GNNs]], [[Neural Graph Collaborative Filtering (NGCF)]], [[LightGCN]]

## Definition

**Graph Neural Networks (GNNs)** are a class of deep learning models that operate on graph-structured data by iteratively aggregating information from a node's neighbourhood to learn rich node representations.

> [!info] Key Intuition
> A node's representation is updated by aggregating the representations of its neighbours, and their neighbours, and so on. After $k$ layers, each node's representation encodes the structure of its $k$-hop neighbourhood.

## Core Concept: Neighbourhood Aggregation

For node $v$ at layer $l$:
1. **Aggregate** representations from all neighbours $\mathcal{N}(v)$
2. **Combine** with current representation
3. **Transform** through a learnable layer

$$h_v^{(l)} = \text{UPDATE}\left(h_v^{(l-1)},\ \text{AGGREGATE}\left(\{h_u^{(l-1)} : u \in \mathcal{N}(v)\}\right)\right)$$

## GNN Variants

| Model | Aggregation | Update |
|---|---|---|
| GCN | Normalised mean | Linear transform + ReLU |
| GraphSAGE | Mean / LSTM / max-pooling | Concatenate + transform |
| GAT | Weighted mean (attention weights) | Transform |
| [[LightGCN]] | Normalised mean (no transform) | Identity |

## GNNs for Recommendation

In recommendation, the graph is a **user-item bipartite graph**:
- Nodes: users and items
- Edges: interactions (clicks, purchases, ratings)
- Goal: learn user/item embeddings from graph structure for CF

> [!example]- Bipartite Graph CF
> User A is connected to Items 1, 2, 3. Item 2 is also connected to User B and User C.
> GNN propagates: User A's embedding gets information from Items 1,2,3; those items' embeddings carry information from their other users. After 2 layers, User A's representation encodes "what other users who liked similar items also liked."

## Significance

GNNs can capture **high-order connectivity** (friends-of-friends relationships) that plain CF ignores, leading to better recommendations especially for sparse user-item matrices where direct co-occurrences are rare.
