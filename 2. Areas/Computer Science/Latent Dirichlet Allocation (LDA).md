**Tags:** #concept #nlp #topic-modelling #bayesian
**Related:** [[Topic Modelling]], [[Dirichlet Distribution]], [[Latent Semantic Analysis (LSA)]], [[LSA vs LDA]]

## Definition

Latent Dirichlet Allocation is a hierarchical probabilistic generative model for collections of documents. Each document is a mixture over $K$ latent topics, each topic is a probability distribution over the vocabulary, and both mixtures are drawn from Dirichlet priors.

> [!info] Key Intuition
> "Topics generate words; documents are mixtures of topics." LDA does not just compress the term–document matrix — it tells a complete story of how every word in every document was produced.

## Generative Process

For $K$ topics, $D$ documents, and vocabulary size $V$:

- For each topic $k = 1, \dots, K$: draw a word distribution
$$\boldsymbol{\phi}_k \sim \text{Dir}(\boldsymbol{\beta}).$$
- For each document $d = 1, \dots, D$: draw a topic mixture
$$\boldsymbol{\theta}_d \sim \text{Dir}(\boldsymbol{\alpha}).$$
- For each word position $n$ in document $d$:
$$z_{dn} \sim \text{Mult}(\boldsymbol{\theta}_d), \qquad w_{dn} \sim \text{Mult}(\boldsymbol{\phi}_{z_{dn}}).$$

Observed: $w_{dn}$. Latent: $z_{dn}, \boldsymbol{\theta}_d, \boldsymbol{\phi}_k$.

## Interpreting the Hyperparameters

| Parameter | Controls | Small value | Large value |
|---|---|---|---|
| $\boldsymbol{\alpha}$ | document–topic concentration | each doc focuses on few topics | each doc mixes many topics |
| $\boldsymbol{\beta}$ | topic–word concentration | sharp topics, few high-prob words | diffuse topics |

> [!example]- Worked Example
> $K=2$, vocabulary $\{\text{market}, \text{price}, \text{cell}, \text{protein}\}$.
> Topic 1 = $(0.45, 0.45, 0.05, 0.05)$ ("economics"). Topic 2 = $(0.05, 0.05, 0.45, 0.45)$ ("biology").
> Document with $\boldsymbol{\theta}_d = (0.8, 0.2)$ → mostly economic words, occasionally biological.

## What "Latent" and "Allocation" Mean

- **Latent**: topics $\boldsymbol{\phi}_k$ and per-word assignments $z_{dn}$ are not observed; they must be inferred.
- **Dirichlet**: both per-document and per-topic distributions have Dirichlet priors (see [[Dirichlet–Multinomial Conjugacy]]).
- **Allocation**: the model assigns (allocates) each token to a latent topic.

## Significance

LDA is the **culmination of classical distributional NLP**: it refines the counting paradigm to its probabilistic limit. But it still operates under Bag-of-Words — word order and context are ignored, and every occurrence of a word shares the same topic distribution. This static-meaning ceiling is exactly what neural embeddings and transformers were built to break.

> [!warning] Common Misconception
> LDA is not clustering. A document is not assigned to one topic — it is a *mixture*. Likewise a word is not owned by one topic — its probability is non-zero in every topic, just sharply higher in some.
