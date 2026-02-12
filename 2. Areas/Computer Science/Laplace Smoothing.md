**Tags:** #concept #nlp
**Related:** [[Naïve Bayes]]

## Definition
Laplace smoothing (also called add-one smoothing) is a technique used in Naïve Bayes to prevent the probability of unseen words from becoming zero.

## Core Mechanics
If a word appears in the test set but never appeared in the training data for a specific class, its probability $P(word|Class)$ would be 0. 

Because Naïve Bayes multiplies these probabilities, a single zero would force the entire document probability to zero.

### Formula
$$ P(w_i | Class) = \frac{count(w_i, Class) + \alpha}{count(Class) + \alpha |V|} $$

Where:
- $\alpha$ is the smoothing parameter (usually 1).
- $|V|$ is the total vocabulary size.

### What is actually done
1. **Hallucinate Counts:** We add $\alpha$ to the observed count of *every* word in the vocabulary for each class. Even if a word was never seen, its count becomes $\alpha$ (usually 1).
2. **Normalize Denominator:** To ensure the sum of probabilities for the class still equals 1, we add $\alpha \times |V|$ to the total count of words in that class.
3. **Assign Small Probabilities:** Unseen words are now assigned a very small, non-zero probability, preventing the "zero-out" effect during multiplication.

## Significance
Smoothing ensures that the model is robust to rare or new words and prevents a single missing word from completely discarding a classification decision.
