**Tags:** #concept #reco
**Related:** [[Graph Neural Networks]], [[DKN for News Recommendation]], [[Collaborative Filtering]]

## Definition

A **Knowledge Graph (KG) for recommendation** is a directed heterogeneous graph of entities (items, genres, directors, attributes) and relations (has_genre, directed_by, belongs_to) that provides external semantic information to augment collaborative filtering signals.

> [!info] Key Intuition
> CF alone says "users who liked Item A liked Item B." A KG adds: "Item A and Item B are both directed by Christopher Nolan and both belong to the Sci-Fi genre." This semantic connection strengthens the recommendation signal even for item pairs with few shared users.

## Structure

$$\mathcal{KG} = \{(h, r, t) | h, t \in \mathcal{E},\ r \in \mathcal{R}\}$$

Where:
- $\mathcal{E}$ = entities (items, people, attributes, concepts)
- $\mathcal{R}$ = relation types
- $(h, r, t)$ = triplet: head entity has relation $r$ to tail entity $t$

> [!example]- Movie Knowledge Graph Triplets
> (Inception, directed_by, Christopher Nolan)
> (Inception, has_genre, Sci-Fi)
> (Inception, stars, Leonardo DiCaprio)
> (The Dark Knight, directed_by, Christopher Nolan)

## How KGs Are Used

1. **Entity embeddings** (TransE, TransR): learn embeddings for all KG entities and relations; use item entity embeddings in the recommender
2. **Path-based methods**: exploit KG paths connecting users and items as meta-paths for CF
3. **Propagation-based methods** (KGCN, KGAT): propagate KG information through GNN layers, combining CF and semantic signals
4. **Hybrid** ([[DKN for News Recommendation]]): use KG entity embeddings as knowledge-enriched item representations

## Benefits

| Benefit | Description |
|---|---|
| Cold start | New items with KG connections can be recommended before any interactions |
| Explainability | "Recommended because both items share director X and genre Y" |
| Diversity | KG paths reveal non-obvious connections |
| Long-tail coverage | Rare items benefit from KG connections to popular entities |

## Significance

Knowledge graphs are widely used in e-commerce (product attributes), news recommendation (entity extraction), and music recommendation (artist/genre graphs). They provide the interpretable semantic backbone that pure CF lacks.
