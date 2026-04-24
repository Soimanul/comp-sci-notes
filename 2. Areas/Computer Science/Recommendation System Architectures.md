**Tags:** #concept #reco
**Related:** [[Recommendation System Overview]], [[Matrix Factorization]], [[AB Testing]]

## Definition

**Recommendation system architectures** are the infrastructure patterns used to serve recommendations to users at scale. Three main patterns exist, each with different latency, freshness, and complexity trade-offs.

> [!info] Key Intuition
> The architecture determines *when* recommendations are computed relative to when they are served. Batch computes everything ahead of time; real-time computes on-demand; 2-step combines both for the best of accuracy and freshness.

## Three Main Architectures

### Batch Architecture

Recommendations are computed **offline** for all users and cached. Requests are served by fetching pre-computed results.

**Pipeline**: Data (GB–TB) → Databricks (model training + recommending) → CosmosDB cache → Kubernetes serving

- **Pros**: Very fast serving latency, handles massive scale.
- **Cons**: Stale recommendations; cannot react to real-time user behaviour; cold users must wait for next batch run.

### Real-Time Architecture

Recommendations are scored and ranked **on the fly** at request time, using a served ML model.

**Pipeline**: Data (MB–GB) → Databricks (feature engineering + model training) → AzureML Service (model serving) → Kubernetes

- **Pros**: Fresh recommendations incorporating the user's most recent actions.
- **Cons**: Higher serving latency; smaller data volume practical; more infrastructure complexity.

### 2-Step (Hybrid) Architecture

A two-stage pipeline: a **retrieval stage** (high recall, fast, batch) produces a large candidate set, then a **ranking stage** (more accurate, real-time) reranks a small subset.

**Pipeline**: Data → Batch retrieval → 100–1000 candidates cached → Real-time reranking (AzureML) → Kubernetes

- **Pros**: Scales to billions of items; allows complex ranking models on small candidate sets.
- **Cons**: Most complex to build and maintain; retrieval errors limit ranking quality.

> [!example]- Industry Example
> YouTube uses a 2-step architecture: a lightweight candidate generation model retrieves hundreds of videos from billions, then a separate ranking neural network scores those candidates for the final feed.

## Significance

Choosing the right architecture is as important as choosing the right model. At industrial scale, batch + 2-step architectures dominate because they decouple the scalability challenge (retrieval) from the accuracy challenge (ranking).
