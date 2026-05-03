**Tags:** #concept #probability #bayesian #topic-modelling
**Related:** [[Dirichlet Distribution]], [[Beta Distribution]], [[Latent Dirichlet Allocation (LDA)]]

## Definition

If the parameter vector of a Multinomial distribution is given a Dirichlet prior,

$$\boldsymbol{\phi} \sim \text{Dir}(\boldsymbol{\alpha}),$$

then after observing word counts $\mathbf{c}$ under that Multinomial, the posterior remains Dirichlet:

$$\boldsymbol{\phi} \mid \text{data} \sim \text{Dir}(\boldsymbol{\alpha} + \mathbf{c}).$$

> [!info] Key Intuition
> Counts simply add to the Dirichlet pseudo-counts. The prior and posterior live in the same family — that is what conjugacy buys you: closed-form Bayesian updating without integration.

## The Dirichlet–Multinomial Marginal

If we **integrate out** the parameter $\boldsymbol{\phi}$ entirely, the resulting marginal distribution over counts is the **Dirichlet–Multinomial** (also called the multivariate Pólya distribution):

$$P(\mathbf{c} \mid \boldsymbol{\alpha}) = \int \text{Mult}(\mathbf{c} \mid \boldsymbol{\phi}) \, \text{Dir}(\boldsymbol{\phi} \mid \boldsymbol{\alpha}) \, d\boldsymbol{\phi}.$$

This induces **dependencies between outcomes**: counts no longer behave independently because they share a common latent parameter that has been marginalised out.

## Significance

This latent coupling is what makes [[Latent Dirichlet Allocation (LDA)]] work. Inference algorithms like collapsed Gibbs sampling exploit conjugacy to integrate out $\boldsymbol{\theta}_d$ and $\boldsymbol{\phi}_k$ analytically and sample only the discrete topic assignments.

> [!warning] Common Misconception
> Conjugacy is not just a mathematical convenience — it is a structural compatibility between prior and likelihood. Without it, topic-model inference would require expensive numerical integration over high-dimensional simplices.
