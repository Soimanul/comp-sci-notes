**Tags:** #concept #nlp #representation #sparse-representations  
**Related:** [[Sparse Representations]] · [[One-hot Encoding]] · [[Term–Document Matrix]] · [[TF–IDF]] · [[Limits of TF–IDF]]

## Definition
At the core of the BoW sits the assumption that <u>word order</u> and <u>syntactic structure</u> can be temporarily ignored, allowing us to focus on word usage patterns. 

**Bag-of-Words** represents a document as a vector over a vocabulary where each dimension records a token’s **count** (or weighted count), ignoring word order and syntax.

## Mechanism
We may think of it as a natural extension of the unigram model, where instead of determining the probabilities of occurrence, we generate a vector whose components are the frequencies of appearance of each of the words, considered as the features of our vector space.

Consider these two sentences:

> *“The kid ate the cookie”*
> 
> *“The cookie ate the kid”* 

Both will be represented with vectors `[2,1,1,1]`, assuming `['The', 'kid', 'ate', 'cookie']` as our dictionary. We know that the meaning differs, but the model does not!

![[Pasted image 20260128130127.png]]

## What BoW captures well
- Topic-level content and term presence.
- Many retrieval/classification baselines when combined with weighting (TF–IDF).

## What BoW loses
- Word order
- Grammatical roles
- Compositional meaning

## Why BoW is foundational
BoW is the basic vector-space representation that leads directly to:
  - The **term–document matrix** (stack BoW vectors).
  - **TF–IDF** (reweigh BoW features).
  - **LSA** (factorize the weighted matrix).
  - And motivates context-based models (e.g., HAL) that reintroduce locality.
