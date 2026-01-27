**Tags:** #concept #nlp #distributional-semantics  
**Related:** [[Distributional Meaning]] · [[Words vs Documents as Vectors]] · [[What “meaning” means in a vector space]] · [[HAL: Contextual Co-occurrence]] · [[Latent Semantic Analysis (LSA)]]

## Definition
The **distributional hypothesis** states that linguistic items with similar meanings tend to occur in **similar contexts**, so meaning can be approximated from usage patterns.

## Core claim
- Meaning is inferred from **distributional behavior** rather than explicit symbolic definitions.
- “Context” can be defined at different granularities:
  - document-level co-occurrence (term–document statistics)
  - window-based co-occurrence (local context)
  - latent factors (compressed/global structure)

## Operationalization in vector space models
- Represent a word (or document) as a vector of co-occurrence statistics.
- Similarity between vectors approximates semantic similarity.

## Implications
- Enables similarity search and clustering based on usage.
- Explains why sparse statistics can encode semantics once you choose:
  - a context definition,
  - a weighting scheme,
  - and a similarity function.

## Known limitations (scope of what it captures)
- Captures association/topical relatedness well.
- Struggles with:
  - logical properties (negation, quantification),
  - fine-grained sense distinctions without richer context handling.
