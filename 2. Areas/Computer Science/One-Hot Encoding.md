**Tags:** #concept #reco #ml
**Related:** [[User and Item Features]], [[Binarization]], [[Factorization Machines]]

## Definition

**One-hot encoding** is a technique to convert **categorical variables** into a binary vector representation suitable for numerical models. Each unique category becomes a separate binary feature (0 or 1).

For a categorical feature with $k$ possible values, one-hot encoding creates $k$ binary dimensions where exactly one is 1 and the rest are 0.

> [!info] Key Intuition
> Machine learning models operate on numbers. One-hot encoding gives a unique, orthogonal representation to each category — no artificial ordinal relationship is implied (unlike converting "red/blue/green" to 1/2/3 which would wrongly suggest green > blue > red).

## Example

| Category | Red | Blue | Green |
|---|---|---|---|
| Red | 1 | 0 | 0 |
| Blue | 0 | 1 | 0 |
| Green | 0 | 0 | 1 |

## Trade-offs in Recommendation Systems

| Pro | Con |
|---|---|
| Handles any categorical feature | Makes data more **sparse** (adds many zero-filled columns) |
| No ordinal assumption imposed | High cardinality features (e.g., UserID, ItemID) create enormous vectors |
| Compatible with linear models | Memory-intensive at scale |

> [!warning] Common Misconception
> One-hot encoding is fine for low-cardinality features (genres: 20 values) but problematic for high-cardinality features (UserID: millions of values). For high-cardinality cases, **embedding layers** (as used in [[Factorization Machines]] and [[Neural Collaborative Filtering]]) are preferred.

## Significance

One-hot encoding is ubiquitous in recommendation feature engineering, particularly for item metadata (genres, categories) and sparse user features. It is a prerequisite for feeding categorical data into models like Factorization Machines.
