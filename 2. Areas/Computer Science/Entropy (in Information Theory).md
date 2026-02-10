**Tags:** #concept #math #nlp
**Related:** [[Maximum Entropy Classifier]], [[Cross-Entropy Loss]]

## Definition
Entropy is a measure of the average uncertainty or information content in a random variable. In classification, it represents the uncertainty of the predicted label probabilities.

## Core Mechanics
The entropy $H(p)$ of a discrete probability distribution $p$ is defined as:

$$ H(p) = - \sum_{x} p(x) \log p(x) $$

- **High Entropy**: The distribution is uniform; we are highly uncertain (e.g., $P = [0.5, 0.5]$).
- **Low Entropy**: The distribution is peaked; we are confident in our prediction (e.g., $P = [0.99, 0.01]$).

## Significance
The Maximum Entropy principle uses this measure to ensure that a model does not assign more structure to a distribution than the data warrants. Training a classifier often involves minimizing the cross-entropy between the predicted and true distributions, which is equivalent to reducing "surprise."
