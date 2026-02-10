**Tags:** #concept #nlp
**Related:** [[Logistic Regression]], [[Entropy (in Information Theory)]], [[Cross-Entropy Loss]]

## Definition
Cross-entropy minimization is the standard training objective for probabilistic classifiers. It involves adjusting the model parameters to minimize the "surprise" of the true labels under the model's predicted distribution.

## Core Mechanics
In binary classification, the objective is to minimize the binary cross-entropy (log loss):

$$ \mathcal{L} = - [y \log(\hat{y}) + (1-y) \log(1-\hat{y})] $$

- When the true label $y=1$, we want $\hat{y}$ to be as close to 1 as possible.
- When $y=0$, we want $\hat{y}$ to be as close to 0 as possible.

## Significance
Minimizing cross-entropy is equivalent to maximizing the likelihood of the observed data. In the context of Maximum Entropy models, this reduction of surprise on observed data leads to a model that is consistent with the data while maintaining maximum uncertainty (entropy) elsewhere.
