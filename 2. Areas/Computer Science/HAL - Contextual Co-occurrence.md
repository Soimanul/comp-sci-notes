**Tags:** #concept #nlp #distributional-semantics #co-occurrence  
**Related:** [[Distributional Hypothesis]] · [[Bag-of-Words (BoW)]] · [[Polysemy]] · [[LSA vs HAL - global vs local structure]]

## Definition
**HAL (Hyperspace Analogue to Language)** represents words using a **contextual co-occurrence matrix** built from a sliding window over text, where a word’s meaning is derived from the words that appear near it.

## Core mechanism
- Slide a window of fixed size over the corpus.
- For each target word, count co-occurrences with context words within the window.
- Often apply a distance-based weighting so nearer words contribute more than farther words.

## What HAL captures
- Local context relationships that document-level BoW statistics can miss.
- Asymmetric or directional associations (depending on how the matrix is constructed), which can encode richer relations than symmetric term overlap.

## Why it helps (relative to document-level vectors)
- Document-level co-occurrence conflates many contexts into one global count.
- Window-based co-occurrence preserves locality, which can help separate senses in cases of [[Polysemy]] and capture more precise associations.

## Strengths
- Aligns directly with the [[Distributional Hypothesis]] by making “context” explicit and local.
- Produces word representations useful for similarity and association tasks.

## Limitations
- Sensitive to window size and weighting choices.
- Still relies on surface co-occurrence and can be sparse without smoothing or dimensionality reduction.
- Typically models words (lexical semantics) more directly than document retrieval unless extended.

## Place in the pipeline
HAL is a “local context” method. Compare with LSA’s global latent factorization in [[Latent Semantic Analysis (LSA)]] and [[LSA vs HAL - global vs local structure]].
