**Tags:** #concept #nlp #representation #sparse-representations  
**Related:** [[Sparse Representations]] · [[One-hot Encoding]] · [[Term–Document Matrix]] · [[TF–IDF]] · [[Limits of TF–IDF: synonymy and polysemy]]

## Definition
**Bag-of-Words** represents a document as a vector over a vocabulary where each dimension records a token’s **count** (or weighted count), ignoring word order and syntax.

## Construction (conceptual)
- Start from one-hot token identities.
- Aggregate over a document:
  - counts per vocabulary item → a single sparse vector.

## Core assumptions
- **Order is irrelevant** for the task: “what words occur” matters more than “where they occur”.
- Words contribute independently to the document representation (no explicit syntax/structure).

## What BoW captures well
- Topic-level content and term presence.
- Many retrieval/classification baselines when combined with weighting (TF–IDF).

## What BoW loses (canonical failure)
- Word order, grammatical roles, compositional meaning.
- Example: “the kid ate the cookie” vs “the cookie ate the kid” produce the same BoW vector.

## Why BoW is foundational
- BoW is the basic vector-space representation that leads directly to:
  - the **term–document matrix** (stack BoW vectors),
  - **TF–IDF** (reweight BoW features),
  - **LSA** (factorize the weighted matrix),
  - and motivates context-based models (e.g., HAL) that reintroduce locality.
