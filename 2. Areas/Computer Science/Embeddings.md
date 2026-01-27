**Tags:** #concept #nlp #representation #vector-space-models  
**Related:** [[Vector Space Model (VSM)]] · [[Distributional Hypothesis]] · [[Cosine Similarity]] · [[Vector Databases]] · [[Latent Semantic Analysis (LSA)]]

## Definition
An **embedding** is a dense vector representation of a linguistic unit (word, sentence, document) that encodes information useful for similarity and downstream tasks.

## Embeddings as a representation shift
- Sparse representations (one-hot/BoW) encode identity and frequency explicitly.
- Dense embeddings encode learned patterns in a lower-dimensional continuous space, where similarity corresponds to learned usage/meaning structure.

## What embeddings are used for (operationally)
- Semantic similarity and nearest-neighbor retrieval.
- Clustering and grouping by meaning.
- Serving as features for ranking and classification.

## Relationship to distributional semantics
Embeddings implement the distributional idea that meaning comes from usage, but compress it into a dense space that generalizes beyond exact overlap.

## Failure modes / constraints
- Embeddings are corpus/model-dependent (geometry reflects training data and objective).
- Similarity depends on metric choice and normalization assumptions.
- Dense similarity can miss exact token constraints unless paired with lexical signals (hybrid retrieval).
