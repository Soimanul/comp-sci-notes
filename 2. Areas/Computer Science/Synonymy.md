**Tags:** #concept #nlp #semantics #limitations  
**Related:** [[TF–IDF]] · [[Bag-of-Words (BoW)]] · [[Latent Semantic Analysis (LSA)]] · [[Distributional Hypothesis]]

## Definition
**Synonymy** is the phenomenon where different surface forms refer to the same or very similar meaning (e.g., “car” vs “automobile”).

## Why synonymy breaks lexical vector models
- BoW/TF–IDF rely on **shared tokens** to measure similarity.
- Two documents can be semantically close but have low similarity if they use different words for the same concept.

## Consequence in retrieval
- Query–document matching fails when the query uses a synonym that is absent from the relevant document.
- Similarity scores underestimate relatedness because overlap is the primary signal.

## Typical remedies in the VSM progression
- Latent structure methods such as [[Latent Semantic Analysis (LSA)]] can connect documents via shared latent factors even without direct token overlap.
- Contextual co-occurrence approaches motivated by [[Distributional Hypothesis]] address synonymy by learning similarity from usage patterns.
