**Tags:** #hub #reco #dl
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> Graph Neural Networks model user-item interactions as a bipartite graph and propagate information through high-order connectivity (friends of friends). NGCF and LightGCN are the key architectures. Knowledge graphs provide external semantic connectivity; DKN uses entity embeddings from a knowledge graph for news recommendation.

## Overview

Recommendation data is naturally graph-structured: users and items are nodes, interactions are edges. GNNs can exploit multi-hop connectivity (users who are connected through shared items have implicit similarity) that matrix factorization ignores.

## Knowledge Map

- [[Graph Neural Networks]]
- [[Message Passing in GNNs]]
- [[High-Order Connectivity in GNNs]]
- [[Neural Graph Collaborative Filtering (NGCF)]]
- [[LightGCN]]
- [[Knowledge Graph for Recommendation]]
- [[DKN for News Recommendation]]

> [!question]- Exam Questions
> - What is the key graph structure used in collaborative filtering GNNs?
> - Explain the message passing framework in GNNs: what is aggregated at each layer?
> - What is high-order connectivity and why is it useful for CF?
> - What is the difference between NGCF and LightGCN? What does LightGCN remove and why?
> - How does a knowledge graph augment standard CF?
> - What is the role of entity embeddings in DKN?
