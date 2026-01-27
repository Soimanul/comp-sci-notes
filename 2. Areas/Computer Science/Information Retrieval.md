**Tags:** #concept #nlp #information-retrieval #search  
**Related:** [[Vector Space Model (VSM)]] · [[TF–IDF]] · [[Cosine Similarity]] · [[Vector Databases]] · [[Embeddings]]

## Definition
**Information Retrieval (IR)** is the task of finding and ranking items (documents, repositories, passages) that are most relevant to a user query.

## Core IR problem
Given a query $q$ and a collection $\mathcal{D}$, estimate relevance and return a ranked list:
- retrieve candidates
- score/rank by relevance
- optimize for top-$k$ quality (what users see)

## Classical IR representations
- Sparse lexical models: BoW and [[TF–IDF]] over a corpus matrix.
- Similarity scoring: [[Cosine Similarity]] and related measures.

## Retrieval vs ranking (pipeline view)
- Candidate generation: fast, high-recall retrieval (lexical or vector).
- Reranking: slower, higher-precision scoring on a bounded set.

## Evaluation (common IR framing)
IR is typically evaluated using top-$k$ ranking metrics (e.g., precision-like measures), because user utility is concentrated in the first results.

## Why it matters for NLP
IR is the “deployment setting” for many NLP representations: vector spaces, weighting, latent semantics, and modern embeddings are all justified by improved retrieval quality.
