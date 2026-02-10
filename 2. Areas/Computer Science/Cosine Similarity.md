**Tags:** #concept #nlp #similarity #vector-geometry  
**Related:** [[Geometric View of Meaning]] · [[Normalization: magnitude vs direction]] · [[Vector Space Model (VSM)]] · [[TF–IDF]]

## Definition
**Cosine similarity** measures similarity between two vectors by the cosine of the angle between them: 
$$cos(\theta)=\dfrac{x \cdot y}{\|x\|\|y\|}$$
It emphasizes **direction** rather than magnitude.

## Why it is used in NLP vector spaces 
- Document/word vectors can differ greatly in length (document size, term frequency volume). 
- Cosine reduces sensitivity to raw magnitude, focusing on the pattern of feature weights.

## Interpretation
- 1.0: same direction (max similarity)
- 0.0: orthogonal (no similarity under the chosen features)
- -1.0: opposite direction (rare in nonnegative count-based spaces)

## Relationship to normalization
- If vectors are L2-normalized, cosine similarity becomes the dot product.
- Normalization makes comparisons consistent across documents of different length.

## Common failure modes / caveats
- If the representation is poor (e.g., unweighted BoW with many common terms), cosine can still rank irrelevant items highly.
- This motivates weighting (TF–IDF) and latent structure (LSA) to improve the geometry.
