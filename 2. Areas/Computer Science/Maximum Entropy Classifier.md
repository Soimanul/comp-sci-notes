**Tags:** #concept #nlp
**Related:** [[Logistic Regression]], [[Entropy (in Information Theory)]]

## Definition
A Maximum Entropy (MaxEnt) classifier is a probabilistic model that follows the principle of choosing the probability distribution which has the highest entropy (most uncertainty) among all distributions that satisfy the constraints observed in the training data.

## Core Mechanics
The idea is to "estimate a probability distribution $P(y|x)$ without making unnecessary assumptions."
- We define a set of **Feature Functions** $f_i(x, y)$ that encode properties we care about.
- We require the model's expected value of these features to match the empirical expectations from the training data.
- The solution to this optimization problem is a model in the **Exponential Family** (Softmax):

$$
P(y \mid x) = \frac{1}{Z(x)} \exp\left( \sum_i \lambda_i f_i(x, y) \right)
$$


Where:
- $\lambda_i$ are the learned weights (Lagrange multipliers).
- $Z(x)$ is the normalization constant (partition function).

## Significance
Framing Logistic Regression as a MaxEnt model provides a strong theoretical justification for its use: it is the most "unbiased" model that respects the observed feature-label associations.
