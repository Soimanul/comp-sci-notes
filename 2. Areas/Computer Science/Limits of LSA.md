**Tags:** #concept #nlp #topic-modelling
**Related:** [[Latent Semantic Analysis (LSA)]], [[Topic Modelling]], [[Latent Dirichlet Allocation (LDA)]]

## Definition

LSA decomposes the term–document matrix via SVD to extract latent dimensions that explain variance. These dimensions are **algebraic** (linear combinations of words) — not probability distributions, and not a generative mechanism.

> [!info] Key Intuition
> LSA tells us documents *can* be represented in fewer dimensions; it does not tell us *how* the words inside them were produced. Compression is not explanation.

## What LSA Does Capture

- A $k$-dimensional subspace of word space that maximises variance of document vectors.
- The dominant linear correlation patterns between words and documents.
- Smoothed similarity that rescues some synonymy mismatches.

## What LSA Does Not Capture

- **No generative story**: latent dimensions are not probabilities and cannot be sampled from.
- **No thematic interpretability**: axes are mixtures of words chosen by variance, not by topic coherence; components can be negative.
- **No mechanism for word production**: LSA describes positions, not the process that placed them.
- **Static word identity**: still operates on Bag-of-Words; ignores order and context.

## Significance

The gap LSA leaves — explanation rather than compression — is exactly what motivates [[Topic Modelling]]. Replacing "which linear structure best approximates the data?" with "what hidden components could have generated it?" leads naturally to Dirichlet priors and [[Latent Dirichlet Allocation (LDA)]].
