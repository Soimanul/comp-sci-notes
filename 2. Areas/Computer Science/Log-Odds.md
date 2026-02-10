**Tags:** #concept #math #nlp
**Related:** [[Logistic Regression]], [[Sigmoid Function]]

## Definition
The log-odds (or logit) is the logarithm of the odds ratio. In Logistic Regression, the log-odds of a class are modeled as a linear combination of the input features.

## Core Mechanics
If $p = P(y=1|x)$, the odds are $\frac{p}{1-p}$. The log-odds $z$ are:

$$ z = \log\left( \frac{p}{1-p} ight) = \mathbf{w}^T \mathbf{x} + b $$

The individual **coefficients** $w_i$ represent the evidence for or against a class.
- $w_i > 0$: The feature increases the log-odds (evidence *for* the class).
- $w_i < 0$: The feature decreases the log-odds (evidence *against* the class).

## Significance
Modeling log-odds as linear allows the model to handle features additively while the Sigmoid function ensures the final output is a valid probability between 0 and 1.
