**Tags:** #concept #nlp #semantics #limitations  
**Related:** [[TF–IDF]] · [[Bag-of-Words (BoW)]] · [[Latent Semantic Analysis (LSA)]] · [[HAL - Contextual Co-occurrence]]

## Definition
**Polysemy** is the phenomenon where the same surface form has multiple meanings depending on context (e.g., “bank” as financial institution vs river bank).

## Why polysemy breaks lexical vector models
- BoW/TF–IDF treat a word type as a single feature regardless of sense.
- This conflates different meanings into one dimension, mixing contexts that should be separated.

## Consequence in retrieval
- Queries can retrieve documents matching the wrong sense because the model cannot disambiguate by context.
- Similarity scores can be inflated between unrelated documents that share ambiguous terms.

## Typical remedies in the VSM progression
- Methods that incorporate context (e.g., window-based co-occurrence like [[HAL - Contextual Co-occurrence]]) help distinguish senses by their local usage patterns.
- More advanced contextual embeddings (beyond this classical pipeline) explicitly model sense via context-dependent representations.
