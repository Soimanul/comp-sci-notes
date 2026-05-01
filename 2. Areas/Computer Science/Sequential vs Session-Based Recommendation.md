“**Tags:** #concept #reco
**Related:** [[GRU for Recommendations]], [[LSTM for Recommendations]], [[Transformer for Sequential Recommendations]], [[CNN for Sequential Recommendations]]

## Definition

**Sequential recommendation** models the temporal ordering of a user's full interaction history to predict their next interaction. **Session-based recommendation** operates on a short, anonymous sequence of interactions within a single session, without access to long-term user history.

> [!info] Key Intuition
> A user watching three action movies in a row has a different immediate preference signal than their average long-term taste. Sequential models capture these short-term dynamics. Session-based recommendation is an extreme case where no user identity is available at all.

## Sequential Recommendation

- **Input**: full ordered interaction history $[i_1, i_2, \ldots, i_{t-1}]$ for user $u$
- **Output**: predicted next item $i_t$
- **Key assumption**: recent interactions are more informative than older ones
- **Models**: RNN-based (GRU4Rec), CNN-based (Caser), Transformer-based (SASRec)

## Session-Based Recommendation

- **Input**: current session sequence $[i_1, i_2, \ldots, i_k]$ — no persistent user ID
- **Output**: predict next item $i_{k+1}$ within the session
- **Challenge**: only short context available; must infer intent from few clicks
- **Models**: GRU (NARM), Graph Neural Networks (SR-GNN), BERT-style (BERT4Rec)

## Comparison

| Property | Sequential | Session-Based |
|---|---|---|
| User identity | Known | Anonymous |
| History length | Long (months/years) | Short (minutes/session) |
| Long-term preferences | Modelled | Not available |
| New user cold start | Problematic | Naturally handled |
| Primary challenge | Modelling long-range dependencies | Inferring intent from few items |

> [!example]- Distinguishing Scenario
> E-commerce: A user's 6-month purchase history shows they buy electronics → sequential recommendation.
> The same user's current 10-minute browsing session shows they're looking at baby products → session-based recommendation should override long-term preferences.

## Significance

Both paradigms are essential in production recommendation. Most modern systems combine them, using long-term history for personalisation and short session context for intent detection.
