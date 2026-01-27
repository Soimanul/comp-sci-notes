**Tags:** #concept #nlp #distributional-semantics #vector-space-models  
**Related:** [[Vector Space Model (VSM)]] · [[Distributional Hypothesis]] · [[Geometric View of Meaning]] · [[Cosine Similarity]] · [[Latent Semantic Analysis (LSA)]]

## Definition
In vector-space NLP, “meaning” is operationalized as **patterns of usage** encoded in vectors, where **similar meaning corresponds to similar vectors** under a chosen similarity function.

## Operational view of meaning
- Meaning is treated as something that can be inferred from **how a word/document is used** in a corpus, rather than from symbolic definitions.
- The model does not store “meaning” directly; it stores **statistics** (counts/weights/co-occurrences) from which meaning is inferred.

## Meaning as similarity
- Two items are considered semantically related if their vectors are “close” under a similarity measure (typically cosine).
- This converts semantic questions into geometric ones:
  - “Are these similar?” → compute similarity
  - “What is most related?” → nearest neighbors

## Dependence on representation choices
What “meaning” you get depends on:
- **features** (terms, contexts, windows, latent dimensions)
- **weights** (raw counts vs TF–IDF)
- **granularity** (document-level vs window-level co-occurrence)
- **dimensionality reduction** (none vs LSA)

## Consequences
- VSM meaning is:
  - **graded** (more/less similar, not binary)
  - **context-dependent on the corpus** (different corpora yield different “meanings”)
  - **approximate** (captures association and topical similarity well; struggles with logical/denotational properties)

## Why this framing matters
It explains why later methods exist:
- TF–IDF: makes “meaning” less dominated by common words.
- LSA: captures latent structure beyond surface overlap.
- HAL: makes “meaning” depend on local context co-occurrence rather than only document frequency.
