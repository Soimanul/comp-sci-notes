**Tags:** #hub #nlp #embeddings
**Related:** [[Natural Language Processing]], [[Vector Space Model (VSM)]], [[Distributional Hypothesis]], [[Latent Dirichlet Allocation (LDA)]]

## Overview

Word embeddings replace **count-based** word representations with **dense, learned** vectors. Where Bag-of-Words, TF–IDF, LSA, and LDA all treat the word as an atomic symbol whose meaning is reconstructed indirectly from co-occurrence statistics, embeddings define meaning as a parameter learned by minimising prediction error. The geometry of the embedding space is intrinsic — similarity is encoded in vector inner products, not in shared counts.

> [!abstract]- TL;DR
> Classical distribution collapses under sparsity, synonymy, polysemy, order loss, and compositional interactions. Word2Vec replaces it with the predictive paradigm: each word becomes a learnable vector in $\mathbb{R}^d$, trained so that similar contexts produce similar predictions. Skip-Gram with negative sampling is implicitly factorising a shifted PMI matrix — predictive and count-based methods are not unrelated, but the predictive route scales and generalises better.

## Knowledge Map

### 1. Why Classical Distribution Collapses
- [[Limits of Count-Based Representations]]

### 2. The Predictive Turn
- [[Word2Vec]]
- [[CBOW vs Skip-gram]]
- [[Skip-Gram Objective]]
- [[Negative Sampling]]

### 3. Connections and Interpretation
- [[Word2Vec PMI Equivalence]]
- [[Embedding Geometry and Analogies]]

### 4. Other Embedding Families
- [[GloVe]]
- [[fastText]]

### 5. Evaluation and Limits
- [[Intrinsic vs Extrinsic Evaluation of Embeddings]]
- [[Static Embedding Limits]]

> [!question]- Common Exam Questions
> - Name three structural failures of Bag-of-Words that motivate dense embeddings.
> - Write the Skip-Gram softmax objective and explain why the denominator is computationally prohibitive.
> - State the negative sampling objective. What does it approximate and how?
> - Under what assumptions does Skip-Gram with negative sampling factorise a shifted PMI matrix?
> - Why do static embeddings fail to handle polysemy, and how do contextual models address it?
> - Explain the king − man + woman ≈ queen result geometrically.

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** Word2Vec's central methodological move was:
- A. Compute counts in a more clever way
- B. Recast word representation learning as a *prediction* problem — train vectors that predict context (or are predicted by it)
- C. Add IDF
- D. Replace softmax with sigmoid

> [!success]- Answer
> **B.** The shift from count-based to predictive paradigms is the defining contribution.

**2.** CBOW differs from Skip-gram in that:
- A. CBOW predicts the *center* word from the surrounding context; Skip-gram predicts the *context* from the center
- B. CBOW is unsupervised, Skip-gram is supervised
- C. CBOW uses softmax, Skip-gram uses sigmoid
- D. CBOW handles rare words better

> [!success]- Answer
> **A.** Skip-gram empirically does better on rare words because each word generates many training pairs (one per context word).

**3.** The full softmax over the vocabulary in Skip-gram is computationally prohibitive because:
- A. The denominator $\sum_{w \in V} e^{u_w \cdot v_c}$ requires a pass over the entire vocabulary per training example
- B. Softmax is non-differentiable
- C. The objective is non-convex
- D. PyTorch is slow

> [!success]- Answer
> **A.** O(|V|) per token × billions of tokens is intractable; negative sampling and hierarchical softmax exist to dodge this.

**4.** Negative sampling reformulates the task as:
- A. K binary classification problems per positive pair: distinguish the true context word from k noise words
- B. K-class softmax
- C. Multi-label classification
- D. Regression

> [!success]- Answer
> **A.** This converts an expensive normalization into a cheap sigmoid-based discrimination, sampling negatives from a unigram^¾ distribution.

**5.** The Levy-Goldberg result shows Skip-gram with negative sampling implicitly factorizes:
- A. A shifted PMI matrix (PMI − log k)
- B. The TF–IDF matrix
- C. The term-document matrix
- D. Identity

> [!success]- Answer
> **A.** A formal bridge between predictive and count-based methods.

**6.** *king − man + woman ≈ queen* works because:
- A. The trained embedding space encodes a roughly linear gender direction; subtracting *man* and adding *woman* shifts along it
- B. Words form a circle
- C. The classifier was trained on royalty
- D. Word2Vec learns rules

> [!success]- Answer
> **A.** Analogies emerge as approximate parallelograms in the embedding space — a property of the learned geometry.

**7.** A *static* embedding's fundamental limit is:
- A. One vector per word, regardless of context — *bank* (river) and *bank* (finance) collapse to the same point
- B. They are too small
- C. They cannot be visualized
- D. They are unsupervised

> [!success]- Answer
> **A.** This is exactly the failure mode that contextual embeddings (ELMo, BERT) solve.

**8.** GloVe differs from Word2Vec in that it:
- A. Explicitly factorizes a global word-word co-occurrence matrix using a weighted least-squares objective
- B. Is supervised
- C. Predicts the next sentence
- D. Uses no co-occurrence statistics

> [!success]- Answer
> **A.** GloVe combines the global statistics of LSA with the locality of Word2Vec.

**9.** fastText extends Word2Vec by:
- A. Representing each word as the *sum of its character n-gram* embeddings, giving compositional handling of OOVs
- B. Using attention
- C. Using transformers
- D. Removing the softmax

> [!success]- Answer
> **A.** Subword n-grams let fastText embed unseen and morphologically related words.

**10.** Why do Word2Vec analogies often *break* on rare words?
- A. Rare words have noisy embeddings due to limited training signal
- B. Word2Vec is incompatible with rare words
- C. Negative sampling deletes them
- D. They have no embeddings

> [!success]- Answer
> **A.** Rare words appear in too few contexts; their vectors fail to settle into the geometry that supports the parallelogram structure.

**11.** *Intrinsic* evaluation of embeddings measures:
- A. Performance on word similarity, analogy, and clustering tasks defined directly on the vectors
- B. Downstream task performance
- C. Inference speed
- D. Vocabulary size

> [!success]- Answer
> **A.** Intrinsic = property of the geometry. Extrinsic = downstream performance (NER, parsing, etc.).

**12.** *Extrinsic* evaluation measures:
- A. Improvement on a downstream NLP task when using the embeddings as features
- B. Cosine similarity statistics
- C. PCA variance
- D. Vocabulary size

> [!success]- Answer
> **A.** Extrinsic answers the practitioner's actual question: do these embeddings make my task better?

**13.** Bias in word embeddings (e.g., *programmer−man+woman ≈ homemaker*) arises because:
- A. The training corpus reflects societal biases; embeddings learn whatever statistical patterns are present
- B. The optimizer is biased
- C. Negative sampling injects bias
- D. Bias is intentional

> [!success]- Answer
> **A.** "Garbage in, geometry out" — embeddings inherit corpus biases; mitigation requires data, debiasing, or downstream filtering.

**14.** Why does Skip-gram with negative sampling perform better on rare words than CBOW?
- A. Each occurrence of a rare word generates many (center, context) training pairs — the rare word receives more gradient updates
- B. CBOW cannot represent rare words
- C. Skip-gram is faster
- D. CBOW does not use negative sampling

> [!success]- Answer
> **A.** Skip-gram amortizes signal across context words.

**15.** Cosine similarity is the standard similarity metric for embeddings because:
- A. The training objective normalizes magnitudes implicitly; angle, not magnitude, encodes meaning
- B. It is faster than dot product
- C. It uses softmax
- D. It is invariant to dimension

> [!success]- Answer
> **A.** Word2Vec / GloVe vectors carry meaning in direction; magnitude reflects frequency-related artifacts.

**16.** Sub-sampling of frequent words during Word2Vec training does what?
- A. Stochastically drops occurrences of high-frequency words to reduce dominance of *the/of/and* and improve rare-word learning
- B. Removes stopwords entirely
- C. Lowercases tokens
- D. Discards the corpus

> [!success]- Answer
> **A.** A heuristic from Mikolov et al. — improves both speed and quality.

**17.** The PMI matrix has the issue that:
- A. PMI is undefined / negative-infinite for never-co-occurring word pairs; PPMI clips negatives to 0
- B. It is too small
- C. It is supervised
- D. It cannot be computed

> [!success]- Answer
> **A.** PMI = log(P(w,c)/(P(w)P(c))) — zeros in the joint produce −∞; PPMI = max(PMI, 0).

**18.** Why are dense embeddings preferred over PPMI vectors despite both encoding distributional information?
- A. Dense low-dimensional vectors generalize better, store cheaper, and integrate seamlessly with neural models
- B. PPMI is wrong
- C. Dense vectors are sparse
- D. PPMI cannot be cosine-compared

> [!success]- Answer
> **A.** 300-dim dense vectors are tractable inputs to downstream models; high-dim sparse vectors are not.

**19.** A linguist demands evaluation of an embedding's *morphological* sensitivity. Which embedding family handles this *best*?
- A. fastText (character n-grams)
- B. One-hot
- C. Word2Vec
- D. LSA

> [!success]- Answer
> **A.** Subword decomposition makes morphology explicit in the representation.

**20.** A trained embedding shows *cat* and *dog* much closer than *cat* and *carburetor*. This reflects:
- A. The distributional hypothesis at work — *cat* and *dog* share contexts (pets, animals); *carburetor* shares contexts with *engine*, *valve*
- B. Random initialization
- C. Overfitting
- D. The optimizer

> [!success]- Answer
> **A.** Geometry encodes which words "keep similar company."

**21.** Which task is *least* well served by static embeddings?
- A. Word-level synonym detection
- B. Word-sense disambiguation in context
- C. Bilingual lexicon induction
- D. Document clustering

> [!success]- Answer
> **B.** WSD requires per-occurrence representations; static embeddings give one vector regardless of sense.

**22.** The deepest reason word embeddings *succeed* is:
- A. They turn the qualitative distributional hypothesis into a geometric, gradient-trainable objective — letting downstream models reuse it
- B. They are unsupervised
- C. They use softmax
- D. They are dense

> [!success]- Answer
> **A.** "Words are known by their company" became "words are vectors learned from contexts" — and the resulting geometry plugs into every downstream model.
