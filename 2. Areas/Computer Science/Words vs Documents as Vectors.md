	**Tags:** #concept #nlp #vector-space-models #distributional-semantics  
**Related:** [[Term–Document Matrix]] · [[Distributional Hypothesis]] · [[Cosine Similarity]] · [[TF–IDF]] · [[Latent Semantic Analysis (LSA)]]

## Definition
In classical vector space NLP, both **documents** and **words** can be represented as vectors; the difference is which axis of the corpus matrix is treated as the vector representation.

## Document vectors
- A document is represented by its term feature weights (counts or TF–IDF).
- Two documents are similar if they share informative terms with similar weights.

## Word vectors (distributional view)
- A word can be represented by how it distributes across documents:
  - the word’s vector is its row/column across the corpus.
- Two words are similar if they appear in similar sets of documents (or contexts), even if they never co-occur directly.

## Why the distinction matters
- Document vectors support retrieval and clustering of documents by topic/content.
- Word vectors support distributional similarity and lexical semantics.

## How this connects to later models
- TF–IDF improves both document and word representations by changing weights.
- LSA changes both by projecting into a shared latent space.
- HAL shifts the definition of “context” from documents to local windows, changing what a “word vector” represents.
