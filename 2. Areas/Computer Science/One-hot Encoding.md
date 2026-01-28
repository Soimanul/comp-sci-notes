**Tags:** #concept #nlp #representation #sparse-vectors  
**Related:** [[Sparse Representations]] · [[Bag-of-Words (BoW)]] · [[Term–Document Matrix]] · [[Vector Space Model (VSM)]]

## Definition
**One-hot encoding** represents each token as a vector of length $|V|$ (vocabulary size) with a single 1 at the index of the token and 0 elsewhere. It is a common technique to transform categorical variables into binary ones.

## Mechanism 
Consider the sentence: 

> *“I think it will rain”*, 

then we have the following vectors:

I: `[1,0,0,0,0]`, think: `0,1,0,0,0`, it: `0,0,1,0,0`, will: `0,0,0,1,0`, rain: `[0,0,0,0,1]`.

Therefore, the sentence becomes a 5x5 matrix: 

`[[1,0,0,0,0], [0,1,0,0,0], [0,0,1,0,0], [0,0,0,1,0], [0,0,0,0,1]]`

In general, it will be a 𝑝𝑥𝑞 matrix with 𝑝 being the number of words and 𝑞 being the size of the dictionary.

## What it represents
A one-hot vector is a **categorical identity representation**:
  - it encodes *which word it is*, but encodes no similarity between words.

## Properties
- **High-dimensional and sparse**: exactly one non-zero entry.
- **Orthogonal basis**: different tokens have dot product 0.
- **No semantic structure**: all distinct tokens are equally dissimilar in this representation.   
   
- **Advantages:** 
	- Clean, independent “one-token = one-dimension” encoding.
	- Simple geometry that works well with many linear/probabilistic models (often convex optimization, interpretable weights).
	- Keeps words as discrete symbols.
       
- **Disadvantages:** 
	- Scales poorly to large vocabularies (very high-dimensional, sparse, memory/compute heavy).
	- Encodes no similarity/semantics (all different words equally dissimilar).
	- Provides little inductive structure, so models must learn relationships/importance from scratch.
	  
> [!info]
> Given this we may think that this encoding has disappeared from modern NLP, but that would not be true… it has actually been hidden.
 >
 >Word embeddings, neural networks, and transformers all start from discrete tokens that are initially treated as orthogonal symbols.
>
  The embedding layer is, in effect, a learned transformation of a one hot vector into a dense space.

## Why it still matters
It is the conceptual base of sparse NLP representations and helps explain:
  - how Bag-of-Words arises from aggregating token identities,
  - why TF–IDF is a reweighing of the same feature space,
  - why dense embeddings can be viewed as a learned transformation from token identities into a lower-dimensional space.

## Limitations
- Vocabulary growth increases dimensionality linearly.
- Captures neither synonymy (different words, similar meaning) nor polysemy (same word, multiple senses).
- Inefficient for similarity search without additional structure (weighting, factorization, or learned embeddings).


