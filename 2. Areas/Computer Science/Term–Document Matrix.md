**Tags:** #concept #nlp #information-retrieval #matrix-representations  
**Related:** [[Bag-of-Words (BoW)]] · [[Distributional Hypothesis]] · [[TF–IDF]] · [[Latent Semantic Analysis (LSA)]]

## Definition
Once text is represented as a Bag-of-Words, it can be encoded numerically into a larger matrix structure.

A **term–document matrix** is a matrix representation of a corpus where entries encode the association between **terms** and **documents**, typically as counts or weighted counts. 

## Orientation 
Two equivalent conventions exist:
- **Term–document:** `rows = terms (words)`, `columns = documents`  
- **Document–term:** `rows = documents`, `columns = terms (words)`

> [!tip] The default choice is the Term-document convention

## Mathematical foundation
In these models each word 𝑤𝑖 is represented by a vector:
$$\vec{w}_i = (X_{i1}\ , X_{i2}\ , \cdots\ , X_{in})$$
This implies that words with similar usage patterns will have similar vectors, consequently words that occur in similar contexts tend to have similar meanings.

> [!info]
Additionally, similarity computations (cosine, etc.) and weighting schemes operate on this matrix representation.

## Conceptual consequences
- The matrix is usually **sparse** (large vocabulary, most terms absent in most documents).
- It supports distributional semantics:
  - terms with similar distributions across documents become similar vectors.
  - documents with similar term distributions become similar vectors.

## What it enables next
- **TF–IDF**: reweight the matrix to reduce common-term dominance.
- **LSA**: factorize the matrix to discover latent structure and reduce dimensionality.
