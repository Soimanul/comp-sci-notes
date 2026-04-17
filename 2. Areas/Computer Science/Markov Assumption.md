**Tags:** #concept #statistics #nlp #rl
**Related:** [[N-gram Model]], [[Markov Chain]], [[Markov Decision Process]]

## Definition
A simplifying assumption used in sequence modeling. It states that the probability of a future state depends **only** on the current state (or a limited history), not on the entire history of events.

## In NLP
For an N-gram model, the Markov assumption approximates the probability of a word by looking only at the last $N-1$ words, rather than the start of the document.
$$P(w_i | w_1...w_{i-1}) \approx P(w_i | w_{i-n+1}...w_{i-1})$$

## In Reinforcement Learning

The Markov property is the foundational assumption of [[Markov Decision Process|MDPs]]: the next state $S_{t+1}$ and reward $R_{t+1}$ depend only on the current state $S_t$ and action $A_t$, not on the full trajectory $S_0, A_0, \ldots, S_{t-1}, A_{t-1}$.

$$p(s', r \mid s, a) = P(S_{t+1}=s', R_{t+1}=r \mid S_t=s, A_t=a)$$

See [[Markov Chain]] for the stochastic-process foundations and [[Markov Decision Process]] for the full RL formalism.