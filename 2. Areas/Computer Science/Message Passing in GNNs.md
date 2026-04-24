**Tags:** #concept #dl
**Related:** [[Graph Neural Networks]], [[High-Order Connectivity in GNNs]], [[Neural Graph Collaborative Filtering (NGCF)]], [[LightGCN]]

## Definition

**Message passing** is the computational framework underlying most GNNs. At each layer, every node sends a **message** (a function of its embedding) to its neighbours, then **aggregates** received messages, and **updates** its own embedding.

> [!info] Key Intuition
> Nodes communicate their current state to neighbours. After $k$ rounds, each node's state reflects the structure of its $k$-hop neighbourhood. This is analogous to belief propagation in probabilistic graphical models.

## Message Passing Framework (MPNN)

For node $v$ at layer $l$:

$$m_v^{(l)} = \text{AGGREGATE}\left(\left\{ \text{MSG}(h_u^{(l-1)}, h_v^{(l-1)}, e_{uv}) : u \in \mathcal{N}(v) \right\}\right)$$

$$h_v^{(l)} = \text{UPDATE}\left(h_v^{(l-1)},\ m_v^{(l)}\right)$$

where $e_{uv}$ = optional edge feature.

## Common Choices

| Function | Description |
|---|---|
| MSG: identity | Pass raw embedding $h_u$ |
| MSG: linear | $W \cdot h_u$ |
| AGGREGATE: sum | $\sum_{u \in \mathcal{N}(v)} \text{MSG}(u)$ |
| AGGREGATE: mean | $\frac{1}{|\mathcal{N}(v)|} \sum$ |
| AGGREGATE: max | $\max_{u \in \mathcal{N}(v)}$ |
| UPDATE: concat+linear | $W \cdot [h_v \| m_v]$ |
| UPDATE: GRU | $\text{GRU}(h_v, m_v)$ |

## GCN Normalisation

Graph Convolutional Networks (Kipf & Welling) normalise messages by degree:

$$h_v^{(l)} = \sigma\left(W^{(l)} \sum_{u \in \mathcal{N}(v) \cup \{v\}} \frac{1}{\sqrt{d_v d_u}} h_u^{(l-1)}\right)$$

where $d_v = |\mathcal{N}(v)|$. The $\frac{1}{\sqrt{d_v d_u}}$ factor prevents high-degree nodes from dominating.

> [!warning] Over-Smoothing
> After many message-passing layers, node representations converge to similar values — high-degree nodes push nearby nodes' embeddings towards a common mean. In practice, 2–3 layers is typically optimal for recommendation GNNs.

## Significance

Message passing is the unifying framework for GCN, GAT, GraphSAGE, NGCF, and LightGCN. Understanding it makes it straightforward to compare these models — they differ only in their choice of MSG, AGGREGATE, and UPDATE functions.
