**Tags:** #concept #reco
**Related:** [[User Item Interaction Model]], [[Explicit Feedback]], [[Negative Sampling in Recommenders]], [[Cold Start Problem]]

## Definition

**Implicit feedback** is data collected from user behaviour without requiring any deliberate rating or review — it is a byproduct of natural interaction with a system.

Examples: clicks, purchases, view/listen time, pointing (hover), impressions, add-to-cart, scroll depth.

> [!info] Key Intuition
> Implicit feedback is **abundant** because it requires no extra effort from the user. Every action a user takes is a data point. The trade-off is that it is **only positive** — you observe what users engaged with, but not what they actively disliked.

## Pros and Cons

| Pros | Cons |
|---|---|
| Often readily available from transaction logs | Often binary (click/no-click) — less granular |
| Not disruptive to users; generates more data points | Hard to define and find true negative samples |
| Less statistical bias; more representative of the full user base | A non-click could mean dislike *or* simply not having seen the item |

## The Positivity Problem

Implicit feedback only records **positive interactions**. Non-interactions are ambiguous:
- The user may have seen the item and disliked it (true negative).
- The user may never have seen the item (missing data, not a preference signal).

This requires [[Negative Sampling in Recommenders]] to construct training negatives artificially.

> [!example]- Example
> A user watches 80% of a YouTube video: strong implicit positive signal. A user sees an ad but does not click: ambiguous — could be dislike, distraction, or irrelevance.

## Significance

Implicit feedback is the dominant data type in production systems because explicit feedback is too sparse. Almost all modern recommendation models (ALS, BPR, NCF) are designed primarily for implicit data.
