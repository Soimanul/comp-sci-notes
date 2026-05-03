**Tags:** #concept #probability #bayesian #topic-modelling
**Related:** [[Beta Distribution]], [[Dirichlet–Multinomial Conjugacy]], [[Latent Dirichlet Allocation (LDA)]]

## Definition

The Dirichlet distribution is a probability distribution **over probability vectors** on the $K$-dimensional simplex. For $\boldsymbol{\theta} = (\theta_1, \dots, \theta_K)$ with $\theta_k \geq 0$ and $\sum_k \theta_k = 1$,

$$p(\boldsymbol{\theta} \mid \boldsymbol{\alpha}) \propto \prod_{k=1}^{K} \theta_k^{\alpha_k - 1}, \qquad \alpha_k > 0.$$

> [!info] Key Intuition
> Dirichlet is to the Multinomial exactly as Beta is to the Binomial. Every sample from a Dirichlet is itself a valid categorical/multinomial distribution — so it is a *distribution over distributions*.

## Effect of the Hyperparameters

The vector $\boldsymbol{\alpha}$ controls how the probability mass spreads across components:

- **Small $\alpha_k$** (e.g. $\alpha_k < 1$): sampled vectors are **sparse** — most mass concentrated on a few components.
- **Large $\alpha_k$**: mass spreads more **uniformly** across all components.

This sparsity control is essential in [[Latent Dirichlet Allocation (LDA)]], where we want each document to focus on a few topics and each topic to focus on a few words.

> [!example]- Worked Example
> $K = 3$ topics with $\boldsymbol{\alpha} = (0.1, 0.1, 0.1)$ → sampled $\boldsymbol{\theta}$ might look like $(0.92, 0.05, 0.03)$ — one dominant topic.
> Same $K$ with $\boldsymbol{\alpha} = (10, 10, 10)$ → typical sample is closer to $(0.34, 0.32, 0.34)$ — near-uniform mixture.

## Significance

The Dirichlet provides the prior that turns the Multinomial Bag-of-Words from a fixed-parameter model into a **hierarchical Bayesian** model. Without it, generative topic modelling cannot encode uncertainty over per-document topic mixtures or per-topic word distributions.
