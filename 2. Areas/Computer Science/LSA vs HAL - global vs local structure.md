**Tags:** #concept #nlp #distributional-semantics #latent-semantics #comparison  
**Related:** [[Latent Semantic Analysis (LSA)]] · [[HAL - Contextual Co-occurrence]] · [[Synonymy]] · [[Polysemy]] · [[Distributional Hypothesis]]

## Core distinction
LSA and HAL both aim to extract semantic structure from co-occurrence patterns, but they differ in **what counts as context** and **how structure is derived**:
- **LSA:** global structure from corpus-wide term–document statistics via factorization.
- **HAL:** local structure from sliding-window co-occurrence statistics.

## LSA (global latent structure)
- Context = document-level distribution across the corpus.
- Mechanism = SVD factorization of a term–document matrix (often TF–IDF).
- Effect = projects words and documents into a latent space that captures broad correlations and reduces sparsity.

## HAL (local contextual structure)
- Context = neighboring words within a fixed window.
- Mechanism = co-occurrence matrix built from windowed counts, often distance-weighted.
- Effect = encodes fine-grained associations and local usage patterns.

## Strength tradeoffs (operational)
- Synonymy: LSA often helps by linking documents/terms through shared latent factors even without overlap.
- Polysemy: HAL can help by conditioning representations on local co-occurrence patterns (less global conflation).
- Granularity: LSA tends toward topical/global similarity; HAL emphasizes local association/usage.

## Practical selection criteria
- Use LSA when the objective is document-level similarity/retrieval and global co-occurrence structure is informative.
- Use HAL when word-level association and local context patterns are the primary signal.

## Relationship rather than replacement
They represent two complementary upgrades over raw BoW:
- LSA: “compress and denoise global usage”
- HAL: “encode local context explicitly”
