**Tags:** #model #nlp #statistics 
**Related:** [[Tokenization]], [[Markov Assumption]]

## Definition
A probabilistic language model that predicts the next item in a sequence based on the $(N-1)$ previous items.

## Probability Calculation
It estimates the probability of a word $w_n$ given a history of words.
$$P(w_n | w_{n-1}, w_{n-2}, ...)$$

## Common Types
- **Unigram (N=1):** Considers each word independently. $P(w)$.
- **Bigram (N=2):** Considers the previous word. $P(w_n | w_{n-1})$.
- **Trigram (N=3):** Considers the previous two words. $P(w_n | w_{n-1}, w_{n-2})$.

## Limitations
- We should be careful since this is not a classification or a regression type of model, therefore we do not predict labels or classes. It predicts the next token in a sequence.

- **Sparsity:** As N increases, the probability of finding that exact sequence in the training data drops to zero.

- **Long-Range Dependencies:** N-grams cannot capture relationships between words that are far apart in the sentence (beyond window N).

## Example with a 1-gram model
Consider the following sentence:

> *“The unhappiness of the players was clearly visible during the final match”*

Now the basic 1-gram model for each of the previous tokenization methods would be.

- **Words**: `[the, unhappiness, of, the, players, was, clearly, visible, during, the, final, match]`

- **Morphemes**: `[the, un-, happy, -ness, of, the, play, -er, -s, was, clear, -ly, visible, during, the, final, match]

- **Subwords**: `[the, un, happi, ness, of, the, play, ers, was, clear, ly, vis, ible, dur, ing, the, final, match]

