**Tags:** #concept #statistics #nlp 
**Related:** [[N-gram Model]]

## Definition
A simplifying assumption used in sequence modeling. It states that the probability of a future state depends **only** on the current state (or a limited history), not on the entire history of events.

## In NLP
For an N-gram model, the Markov assumption approximates the probability of a word by looking only at the last $N-1$ words, rather than the start of the document.
$$P(w_i | w_1...w_{i-1}) \approx P(w_i | w_{i-n+1}...w_{i-1})$$