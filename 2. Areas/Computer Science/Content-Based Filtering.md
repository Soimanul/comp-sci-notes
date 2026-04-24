**Tags:** #concept #reco
**Related:** [[Collaborative Filtering]], [[User and Item Features]], [[Cold Start Problem]], [[Knowledge-Based Recommendation Data]]

## Definition

**Content-based filtering** is a recommendation approach that predicts user preferences based on the **features (content) of users and items**, rather than patterns in collective user behaviour.

> [!info] Key Intuition
> "If Nikhil is in zip code A and age group N and bought item X, then Le in the same area and age group is likely to like X." The model learns what kinds of users prefer what kinds of items, encoded as attribute vectors.

## What "Content" Means

Content can be any attribute data:
- **User features**: age, gender, location, occupation, social connections.
- **Item features**: price, brand, text description, images, genre, style.
- **Review text**: sentiment and topics from written reviews.
- **Knowledge graphs**: structured relationships between entities.
- **Contextual information**: time of day, device, location.
- **Multi-domain data**: images, video, audio features.

## Pros and Cons

| Pros | Cons |
|---|---|
| Handles [[Cold Start Problem]] — works without interaction history | Less personalized than CF when interaction data is abundant |
| Can recommend new items as soon as their features are available | Feature engineering is expensive and domain-specific |
| Explainable: "Recommended because you bought X which has feature Y" | Overspecialization: may never recommend outside known interests |
| Not dependent on other users' behaviour | Features may be incomplete or noisy |

> [!example]- Example
> Spotify's radio feature: recommends songs with similar audio features (tempo, key, energy, instrumentalness) to songs a user has liked. No interaction patterns needed — just audio content embeddings.

> [!warning] Common Misconception
> Content-based filtering does **not** rely on other users' data — it personalises based on the target user's own profile and the item's features. This makes it privacy-preserving but means it cannot discover trends from the broader community.

## Significance

Content-based filtering is essential for cold-start scenarios and is typically combined with collaborative filtering in **hybrid systems** that get the best of both approaches.
