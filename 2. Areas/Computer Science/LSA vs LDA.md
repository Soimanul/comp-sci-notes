**Tags:** #concept #nlp #topic-modelling
**Related:** [[Latent Semantic Analysis (LSA)]], [[Latent Dirichlet Allocation (LDA)]], [[Topic Modelling]]

## Definition

LSA and LDA both extract "latent" structure from a term–document matrix, but the meaning of "latent" is fundamentally different in each: **algebraic** in LSA, **probabilistic** in LDA.

> [!info] Key Intuition
> LSA asks: *what linear directions best explain the variance of word counts?*
> LDA asks: *what hidden distributions could have generated the word counts?*
> The shift is from compression to explanation.

## Side-by-Side Comparison

| Aspect | LSA | LDA |
|---|---|---|
| Mathematical basis | Singular value decomposition | Hierarchical Bayesian model |
| Latent dimensions | Linear combinations of words | Probability distributions over words |
| Document representation | Vector in $\mathbb{R}^k$ | Probability vector over $K$ topics |
| Component values | Real (can be negative) | Non-negative, sum to one |
| Generative? | No — purely descriptive | Yes — defines $P(\text{document})$ |
| Output for new doc | Project onto truncated SVD basis | Posterior inference (e.g. Gibbs) |
| Interpretability of axes | Often opaque mixtures | Topics are word distributions you can read |
| Sparsity control | Implicit via rank $k$ | Explicit via Dirichlet $\alpha, \beta$ |
| Bag-of-Words assumption | Yes | Yes |

## Significance

Both models share the same blind spot: word order is discarded, and meaning is static across occurrences. Neither captures polysemy or compositional structure. The shift from LSA to LDA is therefore a refinement *within* the count-based paradigm — not a transcendence of it. That transcendence requires learned dense representations, which is the conceptual jump to [[Word Embeddings]].

> [!warning] Common Misconception
> "LDA is a probabilistic LSA" is misleading. Probabilistic LSA (pLSA) exists as a halfway model. LDA's distinguishing feature is the Dirichlet prior over both document–topic and topic–word distributions — making it a fully Bayesian generative model.
