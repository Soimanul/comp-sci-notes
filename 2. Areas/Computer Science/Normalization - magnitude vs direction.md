**Tags:** #concept #nlp #vector-geometry #similarity  
**Related:** [[Cosine Similarity]] · [[Geometric View of Meaning]] · [[TF–IDF]] · [[Bag-of-Words (BoW)]]

## Definition
**Normalization** rescales vectors to control how much similarity depends on **magnitude** (length) versus **direction** (feature pattern). In NLP, this is mainly used to reduce the effect of document length and raw count scale.

## Magnitude vs direction
- **Magnitude** reflects scale (e.g., longer documents, higher total counts, more frequent terms).
- **Direction** reflects the relative pattern of features (which terms are emphasized compared to others).

## L2 normalization (most common)
Given a vector $x$, its L2-normalized version is:
$$
\hat{x}=\frac{x}{\|x\|_2}
$$
After L2 normalization, cosine similarity becomes a dot product:
$$
\cos(x,y)=\hat{x}\cdot\hat{y}
$$

## Why normalization matters in text
- Raw count vectors often correlate strongly with document length.
- Without normalization, similarity can be dominated by volume rather than content.
- With normalization, comparisons focus on relative term composition, which aligns better with semantic similarity in many VSM settings.

## Interaction with weighting
- TF–IDF reduces the influence of globally common terms.
- Normalization reduces the influence of document length and scale.
They address different distortions and are often used together.

## Caveats
- Normalization can suppress magnitude signals that are sometimes meaningful (e.g., confidence from repeated evidence).
- The right choice depends on whether “more evidence” should increase similarity or whether similarity should be scale-invariant.
