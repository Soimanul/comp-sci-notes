**Tags:** #concept #probability #bayesian
**Related:** [[Dirichlet Distribution]], [[Topic Modelling]], [[Dirichlet–Multinomial Conjugacy]]

## Definition

The Beta distribution is a continuous probability distribution **over values of a probability** $p \in [0, 1]$. Its density is

$$f(p \mid \alpha, \beta) \propto p^{\alpha - 1}(1-p)^{\beta - 1}, \qquad \alpha, \beta > 0.$$

> [!info] Key Intuition
> The Beta is a *distribution over distributions* in the binary case: each sample from Beta$(\alpha, \beta)$ is itself a valid Bernoulli/Binomial parameter. The hyperparameters $\alpha-1$ and $\beta-1$ behave like prior pseudo-counts of successes and failures.

## Conjugacy with the Binomial

If we place a Beta prior on $p$,

$$p \sim \text{Beta}(\alpha, \beta),$$

and observe $s$ successes and $f$ failures from a Binomial likelihood, the posterior is

$$p \mid \text{data} \sim \text{Beta}(\alpha + s, \beta + f).$$

The posterior has the **same functional form** as the prior — the data updates the parameters by adding counts. This algebraic compatibility is what *conjugacy* means.

> [!example]- Worked Example
> Prior belief that a word's occurrence probability is roughly $0.5$: Beta$(2, 2)$.
> Observe 8 successes out of 10 trials.
> Posterior: $p \mid \text{data} \sim \text{Beta}(10, 4)$ — belief shifts toward higher $p$, with sharper concentration as $\alpha + \beta$ grows.

## Significance

The Beta–Binomial pair is the binary template that the [[Dirichlet Distribution]] generalises to $K$ outcomes. In topic modelling, Beta gives the conceptual bridge from "fixed probability" to "probability as a random variable" — the move that makes Bayesian topic models possible.
