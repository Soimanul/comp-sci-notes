**Tags:** #concept #reco #dl
**Related:** [[Knowledge Graph for Recommendation]], [[Graph Neural Networks]], [[Word Embeddings]]

## Definition

**DKN (Deep Knowledge-Aware Network) for News Recommendation** is a content-based recommendation model that uses entity embeddings from a Knowledge Graph to enrich news article representations, then applies an attention-based neural network to match candidate news against a user's reading history.

> [!info] Key Intuition
> News articles mention real-world entities (people, places, events). DKN maps these entities into a knowledge graph embedding space, enriching the article representation with semantic knowledge beyond its bag-of-words content. A user who reads articles about "Elon Musk" and "SpaceX" has shown interest in those KG entities — DKN uses this signal to recommend related articles.

## Architecture

**Step 1: News encoding (per article)**
- Input: article title words + extracted KG entities + KG context entities
- Multi-channel CNN:
  - Channel 1: word embeddings
  - Channel 2: entity embeddings (from TransE/TransD KG embedding)
  - Channel 3: contextual entity embeddings (one-hop KG neighbours of entities)
- Kim CNN applies filters of multiple sizes → max pooling → article representation

**Step 2: User representation (attention-based)**
- User has read $N$ articles $\{r_1, \ldots, r_N\}$
- **Attention over history**: weight each past article by its relevance to candidate article $c$:
$$a_k = \text{softmax}(\text{score}(e(r_k), e(c)))$$
$$u = \sum_k a_k e(r_k)$$

**Step 3: Prediction**
$$P(\text{click} | u, c) = \sigma(u^T e(c))$$

## Knowledge Graph Entities

Extracted from article titles using entity linking tools. Entity embeddings pre-trained on the news KG using TransE:
$$\mathcal{L}_{KG} = \sum_{(h,r,t)} \max(0, \gamma + d(h+r, t) - d(h'+r, t'))$$

> [!example]- Article Enrichment
> Article: "SpaceX launches Falcon 9"
> Entities: SpaceX (company), Falcon9 (spacecraft), Elon Musk (person)
> KG adds: SpaceX → founded_by → Elon Musk, Falcon9 → is_a → rocket
> The article embedding now incorporates this semantic context.

## Significance

DKN demonstrated that knowledge graph entity embeddings can substantially improve news recommendation by bridging the semantic gap between article content and user preferences. It inspired a family of knowledge-aware recommendation models.
