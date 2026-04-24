**Tags:** #concept #reco
**Related:** [[User Item Interaction Model]], [[Implicit Feedback]], [[User and Item Features]], [[Knowledge-Based Recommendation Data]]

## Definition

The **cold start problem** occurs when a recommendation system cannot make accurate predictions for a **new user** or a **new item** because there is insufficient interaction history.

> [!info] Key Intuition
> A collaborative filtering model learns from past interactions. If there are no past interactions, there is nothing to learn from. Cold start is therefore an inherent weakness of interaction-based methods.

## Two Types of Cold Start

### Cold Users
Users who have not yet provided enough data for accurate recommendations.
- **Cause**: new user to the system, infrequent user, first-time interactions.
- **Example**: a customer who just signed up and has not browsed or bought anything.

### Cold Items
Items that have not been interacted with by enough users.
- **Cause**: new product launches, unique or niche items.
- **Example**: a new film release with no ratings yet; a rare luxury item.

## Mitigation Strategies

| Strategy | How It Helps |
|---|---|
| [[User and Item Features]] | Use demographic/attribute data when interaction data is absent |
| [[Knowledge-Based Recommendation Data]] | Apply domain rules and user requirements |
| Onboarding surveys | Collect explicit preferences from new users upfront |
| Popularity-based fallback | Recommend trending/popular items to cold users |
| Hybrid models | Combine content-based and collaborative filtering |

> [!example]- Example
> Buying a house is a classic cold-start scenario: the user has likely never bought a house before, so there is no interaction history. A knowledge-based system that collects explicit requirements (budget, location, number of rooms) bypasses the problem entirely.

> [!warning] Common Misconception
> The cold start problem is not solved just by having more users — it is a per-user, per-item problem. A system with millions of users still faces cold start for every new item and every new user.

## Significance

Cold start is one of the most practical challenges in production recommendation systems. It directly impacts the experience for new customers and for long-tail items, making feature-based and hybrid approaches essential alongside pure collaborative filtering.
