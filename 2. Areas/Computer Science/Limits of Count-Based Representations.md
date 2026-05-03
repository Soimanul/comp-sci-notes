**Tags:** #concept #nlp #embeddings
**Related:** [[Word Embeddings]], [[Bag-of-Words (BoW)]], [[Latent Semantic Analysis (LSA)]], [[Latent Dirichlet Allocation (LDA)]]

## Definition

Bag-of-Words, TF–IDF, LSA, and LDA all treat each word as an **atomic symbol** — an indivisible token without internal structure, occupying its own dimension. Meaning is reconstructed indirectly from co-occurrence statistics. This atomic view leads to several structural failures that motivate the move to learned dense vectors.

> [!info] Key Intuition
> The problem with count-based models is not computational but **representational**. Even after compression, the underlying representation is still made of orthogonal one-hot dimensions. Similarity has to be inferred *after the fact*, not encoded in the representation itself.

## The Five Structural Failures

### 1. Sparsity
A realistic vocabulary contains tens of thousands of types. Each document vector lives in $\mathbb{R}^V$ but most coordinates are zero. Even LSA's truncated SVD originates from sparse count matrices — it compresses but does not redefine.

### 2. Synonymy
*"car"* and *"automobile"* occupy completely independent dimensions in BoW. Their similarity must be inferred indirectly through shared contexts. LSA partially smooths this; LDA may place them in the same topic — but both rely on global statistical regularities.

### 3. Polysemy
*"bank"* (finance) and *"bank"* (river) share a single representation. LDA may assign different topic mixtures in different documents, but the **word vector itself does not change**. The representation remains static — meaning is averaged across contexts.

### 4. Disappearance of Order
Bag-of-Words treats documents as exchangeable token collections. *"Dog bites man"* and *"Man bites dog"* are identical. LSA and LDA inherit this — neither reintroduces sequence information.

### 5. Negation and Interaction
*"I like this movie"* vs *"I do not like this movie"* differ only by a single token addition. The interaction between *not* and *like* is not structurally represented. **Counts are additive; meaning is not.**

## What This Diagnosis Implies

- Sparsity → the space is the wrong space.
- Synonymy → similarity should be **graded** at the representation level, not reconstructed afterwards.
- Polysemy → meaning must be **dynamic in context**, not a fixed lookup.
- Order loss → composition needs structural support.
- Interaction → independence assumptions kill non-additive phenomena.

## Significance

These five failures map directly onto the design moves of [[Word Embeddings]] and later transformers:

- Sparsity → dense low-dimensional vectors.
- Synonymy → graded geometric similarity by inner product.
- Polysemy → contextual embeddings (BERT, GPT) where the vector for *"bank"* depends on its sentence.
- Order loss → recurrent / attention models that consume sequences.
- Interaction → multi-layer non-linear composition.

This is the conceptual collapse point of classical distributional NLP and the launch point for the predictive paradigm.
