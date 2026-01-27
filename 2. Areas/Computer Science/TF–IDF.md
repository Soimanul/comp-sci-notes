**Tags:** #concept #nlp #information-retrieval #term-weighting  
**Related:** [[Term Frequency (TF)]] · [[Inverse Document Frequency (IDF)]] · [[Cosine Similarity]] · [[Limits of TF–IDF]] · [[Latent Semantic Analysis (LSA)]]

## Definition
**TF–IDF** is a term-weighting scheme that assigns higher weight to terms that are **frequent in a document** but **rare across the corpus**, improving sparse vector representations for similarity and retrieval.

## Canonical weighting
For term $t$ in document $d$:
$$
w(t,d)=tf(t,d)\cdot idf(t)
$$
with $tf$ and $idf$ chosen from standard variants.

## What TF–IDF changes vs raw counts
- Reduces dominance of high-frequency corpus-wide terms (stopword-like behavior without explicitly removing them).
- Increases influence of terms that better distinguish documents.

## How it is used in retrieval
- Documents become TF–IDF vectors.
- Queries are represented in the same space (often as TF–IDF too).
- Similarity is computed with cosine similarity (commonly after normalization):
  - see [[Cosine Similarity]] and [[Normalization: magnitude vs direction]].

## What TF–IDF does not solve
- It does not introduce meaning beyond lexical overlap; it reweights overlap.
- It still struggles with vocabulary mismatch (synonymy) and multiple senses (polysemy):
  - see [[Limits of TF–IDF: synonymy and polysemy]].

## Why it matters in the progression
TF–IDF is the standard improvement over BoW and also the typical input to latent methods like [[Latent Semantic Analysis (LSA)]].
