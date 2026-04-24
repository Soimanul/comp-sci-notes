**Tags:** #concept #reco
**Related:** [[Precision@K]], [[Recall@K]], [[NDCG@K]], [[MAP@K]], [[MAE (Mean Absolute Error)]], [[A/B Testing]]

## Definition

**Offline metrics** are computed on a held-out test set during model development — no live users are involved. **Online metrics** (also called business metrics) are measured in production with real users.

> [!info] Key Intuition
> Offline metrics tell you how well the model performs on a static dataset. Online metrics tell you if the model actually helps the business. A model can have excellent offline metrics but poor online metrics if it optimises the wrong objective.

## Offline Metrics (by task)

| Task | Metric |
|---|---|
| Rating prediction | [[Mean Squared Error (MSE)]], [[MAE (Mean Absolute Error)]], R², AUC |
| Ranking | [[Precision@K]], [[Recall@K]], [[NDCG@K]], [[MAP@K]] |
| Diversity | Novelty, Diversity, Serendipity, Coverage → see [[Diversity Metrics in Recommendation]] |

## Online / Business Metrics

| Metric | Definition |
|---|---|
| CTR (Click-Through Rate) | Clicks ÷ total page views |
| Conversion Rate | Purchases (conversions) ÷ total visits |
| AOV (Average Order Value) | Total revenue ÷ number of orders |
| MAU (Monthly Active Users) | Unique users active in a month |
| LTV (Lifetime Value) | Avg order value × purchases/year × avg retention time |

> [!warning] Common Misconception
> Optimising offline metrics does NOT guarantee improvement in business metrics. A model that perfectly ranks relevant items may still fail to improve CTR if the UI, copy, or placement is wrong. Always validate with [[A/B Testing]] before full deployment.

## Significance

The offline/online metric gap is one of the most common failure modes in ML deployments. Strong offline performance is necessary but not sufficient — online A/B tests are the only way to confirm actual business impact.
