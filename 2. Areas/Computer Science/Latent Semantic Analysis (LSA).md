**Tags:** #concept #nlp #information-retrieval #dimensionality-reduction #latent-semantics  
**Related:** [[TF–IDF]] · [[Term–Document Matrix]] · [[Synonymy]] · [[Polysemy]] · [[LSA vs HAL: global vs local structure]]

## Definition
**Latent Semantic Analysis (LSA)** models documents and terms in a **lower-dimensional latent space** derived from the term–document matrix, aiming to capture underlying semantic structure beyond surface word overlap.

## Core mechanism
- Start with a weighted term–document matrix (often TF–IDF).
- Apply Singular Value Decomposition (SVD) and keep the top $k$ components:
$$
X \approx U_k \Sigma_k V_k^\top
$$
This projects terms and documents into a shared latent space.

## What LSA is trying to solve
- Vocabulary mismatch from [[Synonymy]]: semantically similar documents may use different words.
- Noise/sparsity in high-dimensional lexical spaces.
- Over-reliance on exact overlap in TF–IDF similarity.

## What the latent space represents (operationally)
- Latent dimensions act like “topics” or correlated usage factors, derived from global co-occurrence patterns across the corpus.
- Documents/terms that load similarly on latent factors become close even without direct word overlap.

## Strengths
- Improves retrieval when relevant documents share concepts but not vocabulary.
- Reduces dimensionality, which can denoise similarity computations.

## Limitations
- Latent factors are not guaranteed to be interpretable.
- Global factorization can blur fine-grained distinctions, including some cases of [[Polysemy]].
- Requires selecting $k$ and can be sensitive to corpus/domain shifts.

## Place in the pipeline
LSA is a “global structure” method: it derives semantics from corpus-wide patterns. Compare with the local-context approach in [[HAL: Contextual Co-occurrence]].
