**Tags:** #concept #nlp #information-retrieval #matrix-representations  
**Related:** [[Bag-of-Words (BoW)]] · [[Distributional Hypothesis]] · [[TF–IDF]] · [[Latent Semantic Analysis (LSA)]]

## Definition
A **term–document matrix** is a matrix representation of a corpus where entries encode the association between **terms** and **documents**, typically as counts or weighted counts.

## Orientation (be explicit)
Two equivalent conventions exist:
- **Term–document:** rows = terms, columns = documents  
- **Document–term:** rows = documents, columns = terms  
The choice is not mathematical content; it determines whether “documents” are row vectors or column vectors in downstream formulas.

## What the entries mean
- Basic form: \(X_{t,d}\) = count of term t in document d
- Weighted form: \(X_{t,d}\) = TF–IDF (or other weight) for term t in document d

## Why it is the central object
- Each **document vector** is a column/row of the matrix.
- Each **term vector** is the corresponding row/column across documents.
- Similarity computations (cosine, etc.) and weighting schemes operate on this matrix representation.

## Conceptual consequences
- The matrix is usually **sparse** (large vocabulary, most terms absent in most documents).
- It supports distributional semantics:
  - terms with similar distributions across documents become similar vectors,
  - documents with similar term distributions become similar vectors.

## What it enables next
- **TF–IDF**: reweight the matrix to reduce common-term dominance.
- **LSA**: factorize the matrix to discover latent structure and reduce dimensionality.
