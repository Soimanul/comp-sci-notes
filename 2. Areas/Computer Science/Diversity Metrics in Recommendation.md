**Tags:** #concept #reco
**Related:** [[Offline vs Online Metrics]], [[Recommendation System Overview]]

## Definition

**Diversity metrics** measure the **variety, surprise, and breadth** of recommendations beyond pure accuracy. They capture the "added value" a recommendation system provides beyond simply ranking the most popular items.

> [!info] Key Intuition
> A model that only recommends the most popular items will have high accuracy metrics but will fail users who want to discover new things. Diversity metrics capture this — and help avoid "filter bubbles."

## The Four Core Diversity Metrics

### Novelty
Measures how **novel** (non-obvious) recommendations are by computing the average popularity of recommended items. Less popular items → higher novelty.
- High novelty: surfacing long-tail items.
- Low novelty: always recommending the top 10 most popular items.

### Diversity
Measures how **different items in the recommendation set are from each other**.
- A diverse set contains items from different categories, styles, or topics.
- Computed as average pairwise dissimilarity within the recommended list.

### Serendipity
Measures how **surprising and pleasant** recommendations are — items the user wouldn't have expected but ends up liking. Computed by comparing recommendations to a "relevance baseline" (what a basic model would suggest).

### Coverage
Measures the **proportion of the total item catalogue** that the system recommends across all users.
- Low coverage: only a small fraction of items ever gets recommended (popularity bias).
- High coverage: the long tail is surfaced frequently.

## Accuracy vs Diversity Trade-off

> [!example]- ALS vs Random Recommender
> ALS outperforms a random recommender on ranking metrics (Precision@K, NDCG@K). However, the random recommender outperforms ALS on diversity metrics. ALS is optimised for accuracy, so it tends to recommend popular items repeatedly, leaving the long tail unexplored.

> [!warning] Common Misconception
> Maximising accuracy metrics (NDCG, Precision) can **reduce diversity**. Production systems must balance accuracy and diversity — often using a two-stage pipeline where a diverse candidate set is retrieved and then ranked.

## Significance

Diversity metrics are essential for avoiding filter bubbles and ensuring long-tail items get exposure. They are non-accuracy metrics that measure the broader value a recommendation system provides to both users and the business.
