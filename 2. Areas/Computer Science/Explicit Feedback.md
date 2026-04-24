**Tags:** #concept #reco
**Related:** [[User Item Interaction Model]], [[Implicit Feedback]], [[Cold Start Problem]]

## Definition

**Explicit feedback** is user-generated data that directly and intentionally expresses a preference or opinion about an item.

Examples: numerical star ratings (Netflix, IMDB), survey responses with satisfaction levels, written reviews with positive or negative sentiment.

> [!info] Key Intuition
> Explicit feedback is **gold-standard signal** — the user told you exactly what they think. But it's expensive to collect because it requires the user to take an extra action beyond natural behaviour.

## Pros and Cons

| Pros | Cons |
|---|---|
| More informative and richer | Costly to obtain — requires user effort |
| Easier to interpret for algorithms | Inconvenient to users; many don't bother |
| Can naturally capture negative feedback | Biased towards vocal/extreme users |
| Directly measures preferences | May need calibration (different users use scales differently) |

> [!warning] Common Misconception
> Explicit ratings are not always reliable ground truth. Rating scales are interpreted subjectively: one user's 4/5 may equal another's 3/5. Bias towards certain demographics (English speakers, tech-savvy users) skews the data.

> [!example]- Example
> Netflix's 5-star rating system is explicit feedback. When they switched to thumbs up/down, they got 200% more ratings — showing that lower friction increases data volume, even if it reduces granularity.

## Significance

Explicit feedback is preferred when available because it directly models preferences. However, its scarcity often means models must also rely on [[Implicit Feedback]] to achieve good coverage.
