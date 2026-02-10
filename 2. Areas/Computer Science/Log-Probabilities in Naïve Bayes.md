**Tags:** #concept #nlp
**Related:** [[Naïve Bayes]]

## Definition
Using log-probabilities is a formal transformation in Naïve Bayes to improve numerical stability and computational efficiency.

## Core Mechanics
Naïve Bayes involves multiplying many small probabilities (between 0 and 1). Multiplying these can quickly lead to **numerical underflow**, where the resulting number becomes too small for a computer to represent accurately.

By taking the logarithm of the probabilities, we can convert the products into sums:

$$ \log(P(C) \prod P(w_i|C)) = \log(P(C)) + \sum \log(P(w_i|C)) $$

## Significance
This transformation makes the computation stable and allows for faster calculation using addition instead of multiplication.
