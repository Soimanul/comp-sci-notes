**Tags:** #concept #reco
**Related:** [[User Item Interaction Model]], [[Cold Start Problem]], [[User and Item Features]]

## Definition

**Knowledge-based recommendation data** is structured domain knowledge used when historical interaction data is insufficient or absent. Instead of learning from past behaviour, the system uses explicit user requirements, goals, constraints, or ontologies.

> [!info] Key Intuition
> For high-stakes, infrequent purchases (a car, a house, an insurance plan), users rarely have interaction history. Knowledge-based systems let users specify exactly what they want — making the recommender explainable and reliable even without historical data.

## When to Use

Knowledge-based data is most valuable when:
- Items are **infrequently purchased** (cars, houses, luxury goods).
- User history is too sparse to be useful.
- The domain is **complex** with many constraints (e.g., financial products, medical equipment).
- **Explainability** is required for regulatory or trust reasons.

## Representations

Knowledge can be encoded as:
- **Rules** — "if user wants family car, show minivans and SUVs"
- **Cases** — past successful recommendations with similar requirements
- **Constraints** — price range, required features, geographic limits
- **Knowledge graphs** — ontologies of entities and relationships (e.g., film genres, ingredients)

> [!example]- Example (DKN Paper)
> The DKN paper (WWW 2018) uses a knowledge graph for news recommendation: entities in news articles (people, organisations, locations) are linked via a graph, allowing the model to reason about relationships between news stories rather than relying solely on click history.

> [!warning] Common Misconception
> Knowledge-based systems are not a substitute for interaction-based systems at scale — they are **complementary** and most powerful when combined with collaborative or content-based approaches in hybrid models.

## Significance

Knowledge-based data enables explainable recommendations and solves cold-start scenarios that interaction data cannot. It is particularly important in regulated industries and for high-value purchases.
