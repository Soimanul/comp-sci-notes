**Tags:** #concept #reco
**Related:** [[Interaction Count]], [[Weighted Interaction Count]], [[Weighted Time Decay]], [[Affinity Matrix]]

## Definition

**Time decay** is a data transformation that reduces the **relevance of older interactions**, giving more weight to recent behaviour when computing affinity scores.

The general form applies an exponential decay based on the age of an interaction:

$$\text{affinity}(u, i) = \sum_{t} \exp\!\left(-\frac{t_0 - t}{T}\right)$$

where $t_0$ is the current time, $t$ is the interaction timestamp, and $T$ is a **half-life** parameter.

> [!info] Key Intuition
> User tastes change over time. A movie rating from 5 years ago is less informative about today's preferences than a purchase made last week. Time decay reflects this by treating stale interactions as weaker signals.

## The Half-Life Parameter T

The scaling factor $T$ serves as a half-life: **events $T$ time units before $t_0$ are given half the weight** of events at $t_0$.

- Small T → decay quickly, focus on very recent behaviour.
- Large T → decay slowly, treat older interactions as still relevant.

> [!example]- Example
> Fashion recommendation: tastes drift fast → use small T (decay within weeks). Classic book recommendation: tastes are stable → use large T (decay over years).

## Significance

Time decay is critical in domains with shifting user preferences (fashion, news, music trends). Without it, models overweight historical patterns that no longer represent the user's current interests.
