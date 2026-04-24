**Tags:** #concept #reco
**Related:** [[User Item Interaction Model]], [[Cold Start Problem]], [[Content-Based Filtering]]

## Definition

**User and item features** are attribute data about users and items that complement interaction data. They are the foundation of content-based filtering and help alleviate the cold start problem.

- **User features**: demographics (age, gender, location, occupation), social connections, device type.
- **Item features**: price, brand, category, description text, images, style attributes, release date.

> [!info] Key Intuition
> Features provide context when interaction history is absent or sparse. If a new user provides their age and location, you can recommend to them based on what similar demographic profiles have liked — even before they make their first interaction.

## Pros and Cons

| Pros | Cons |
|---|---|
| Can reveal additional predictive factors (demographics, images) | Usually less personalised than interaction-based signals |
| Valuable when interaction data is sparse | Privacy constraints may limit available user features |
| Allows stratification by user or item characteristics | Features must be carefully engineered |
| Useful for customer segmentation business objectives | Multi-domain data (images, video) increases complexity |

## Feature Types

| User Features | Item Features |
|---|---|
| Age, gender, location, occupation | Color, size, brand, fashion style |
| Social network, followed accounts | Price, category, description |
| Device type, time of day | Release date, ratings, reviews |

> [!example]- Example
> In fashion recommendation, item features (colour, style, brand) are critical because two visually similar items may have very different recommendation outcomes even if their purchase histories are sparse.

## Significance

User and item features are essential when data per user or item is sparse, and they enable content-based filtering approaches that generalise better to new items than pure collaborative methods.
