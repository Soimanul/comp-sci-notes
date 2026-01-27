**Tags:** #concept #ml-systems #vector-search #infrastructure  
**Related:** [[Embeddings]] · [[Information Retrieval]] · [[Cosine Similarity]] · [[Vector Space Model (VSM)]]

## Definition
A **vector database** stores high-dimensional vectors and supports fast similarity search (nearest neighbors) over them, typically via approximate nearest neighbor (ANN) indexing.

## What it stores
- Vectors (embeddings) representing items (documents, repos, queries, chunks).
- Associated metadata (IDs, filters, timestamps, tags).

## What it does
- Nearest neighbor search: return the top-$k$ vectors most similar to a query vector.
- Metadata filtering: restrict search to subsets (e.g., language, activity, license).
- Indexing: builds ANN structures to trade a small accuracy loss for large speed gains.

## Similarity / distance interface
Vector DBs expose ranking by a metric such as:
- cosine similarity (angle-based)
- dot product
- Euclidean distance
The metric choice must match the embedding model’s training/normalization assumptions.

## Why it matters in modern IR
Vector DBs operationalize semantic retrieval by making embedding similarity queryable at scale, enabling “meaning-based” matching beyond exact keyword overlap.
