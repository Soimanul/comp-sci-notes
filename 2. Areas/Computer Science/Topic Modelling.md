**Tags:** #hub #nlp #topic-modelling
**Related:** [[Natural Language Processing]], [[Vector Space Model (VSM)]], [[Latent Semantic Analysis (LSA)]]

## Overview

Topic modelling shifts NLP from **geometric** representation (counts, vectors, matrix factorisation) to **generative probabilistic** modelling. Instead of asking "what linear structure best approximates the data?", topic models ask "what hidden thematic components could have generated the observed word counts?"

> [!abstract]- TL;DR
> Vector space models and LSA describe how documents are positioned, not how they are produced. Topic models like LDA posit hidden topics as probability distributions over words, with each document as a mixture of topics. The Dirichlet distribution provides the conjugate prior over those mixture vectors.

## Knowledge Map

### 1. Why VSM and LSA Are Not Enough
- [[Vector Space Model (VSM)]]
- [[Latent Semantic Analysis (LSA)]]
- [[Limits of LSA]]

### 2. Probability Foundations
- [[Beta Distribution]]
- [[Dirichlet Distribution]]
- [[Dirichlet–Multinomial Conjugacy]]

### 3. The Generative Topic Model
- [[Latent Dirichlet Allocation (LDA)]]
- [[LSA vs LDA]]

> [!question]- Common Exam Questions
> - Why does LSA fail to qualify as a generative model?
> - State the Dirichlet density and explain what its hyperparameters $\alpha_k$ control.
> - Write the LDA generative process for a single document.
> - Compare LSA and LDA: what is "latent" in each?
> - What does it mean to say the Dirichlet is the conjugate prior of the Multinomial?

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** LSA fails to qualify as a *generative* model because:
- A. It is computed via SVD on a count matrix — there is no probabilistic story for how documents are produced
- B. It uses too many topics
- C. SVD requires square matrices
- D. LSA only works on English

> [!success]- Answer
> **A.** SVD is geometric/algebraic; generative models specify $P(\text{document})$ via a sampling process.

**2.** A Dirichlet distribution is parameterized by:
- A. A vector $\boldsymbol{\alpha}$ of positive concentration parameters; it produces probability vectors that sum to 1
- B. A scalar mean
- C. A covariance matrix
- D. A binary indicator

> [!success]- Answer
> **A.** Dir($\boldsymbol{\alpha}$) lives on the simplex — the natural prior for categorical/multinomial distributions.

**3.** Setting all $\alpha_k = 1$ in a Dirichlet yields:
- A. A point mass
- B. The uniform distribution over the simplex
- C. A spike at a corner
- D. A Gaussian

> [!success]- Answer
> **B.** $\alpha = (1, 1, \ldots, 1)$ is the uninformative Dirichlet — every probability vector is equally likely.

**4.** Setting all $\alpha_k < 1$ produces draws that are:
- A. Concentrated near the corners of the simplex (sparse)
- B. Concentrated at the center
- C. Identical to a Beta distribution
- D. Always uniform

> [!success]- Answer
> **A.** Sparsity-inducing prior — most mass on probability vectors with one or two dominant components, which is what we want for documents covering few topics.

**5.** Setting all $\alpha_k > 1$ produces draws that are:
- A. Concentrated at the corners
- B. Concentrated near the center (uniform-like) — every component non-negligible
- C. Negative
- D. Sparse

> [!success]- Answer
> **B.** Large $\alpha$ → smooth, dense mixtures.

**6.** The Beta distribution is the special case of the Dirichlet for:
- A. K=2 (binary outcomes)
- B. K=3
- C. Any K
- D. K=1

> [!success]- Answer
> **A.** Beta($\alpha, \beta$) = Dir($\alpha, \beta$) over a probability $p$ and $1-p$.

**7.** "Conjugate prior" of the Multinomial means:
- A. The posterior, after a multinomial likelihood update, remains Dirichlet — closed-form updates with no integral
- B. They commute under multiplication
- C. They are independent
- D. They are inverse functions

> [!success]- Answer
> **A.** Dirichlet × Multinomial → Dirichlet (with updated parameters), giving the analytical convenience that drives Bayesian topic modelling.

**8.** In LDA, *topics* are formally:
- A. Probability distributions over the vocabulary
- B. Documents
- C. Embeddings
- D. Cluster centroids in vector space

> [!success]- Answer
> **A.** A topic is $\boldsymbol{\beta}_k$ — a multinomial over words. "Football" topic = high probability on *goal, match, league*…

**9.** In LDA, a *document* is:
- A. A mixture of topics; specifically, $\boldsymbol{\theta}_d \sim \text{Dir}(\alpha)$ is a probability distribution over topics
- B. A single topic
- C. A vector of TF–IDF scores
- D. A topic centroid

> [!success]- Answer
> **A.** Each document has its own mixture proportions; words are then sampled topic-then-word.

**10.** The LDA generative process for a single word in document $d$ is:
- A. Sample topic $z \sim \text{Cat}(\boldsymbol{\theta}_d)$, then sample word $w \sim \text{Cat}(\boldsymbol{\beta}_z)$
- B. Sample word from a Gaussian
- C. Sample document from a topic
- D. Compute TF–IDF

> [!success]- Answer
> **A.** Two-step ancestral sampling: pick a topic according to document mixture, then pick a word according to that topic.

**11.** What is "latent" in LDA?
- A. The topic indicator $z$ for each word and the per-document mixture $\boldsymbol{\theta}_d$ — neither is observed
- B. The vocabulary
- C. The document length
- D. The Dirichlet $\alpha$

> [!success]- Answer
> **A.** Inference's job is to estimate these unobserved variables given observed words.

**12.** What is "latent" in LSA?
- A. The truncated singular vectors representing semantic dimensions
- B. The vocabulary
- C. The document IDs
- D. The corpus size

> [!success]- Answer
> **A.** Latent semantic dimensions are the directions of largest variance in the term-document matrix — geometric, not probabilistic.

**13.** A central limit of LSA is:
- A. It produces real-valued (possibly negative) "topic" loadings without an interpretable probabilistic semantics
- B. It is too slow
- C. It cannot scale
- D. It only works on English

> [!success]- Answer
> **A.** Negative values in LSA topics resist interpretation; LDA produces non-negative probabilities by construction.

**14.** Approximate inference for LDA typically uses:
- A. Variational inference or collapsed Gibbs sampling
- B. Closed-form solutions
- C. SVD
- D. Backpropagation

> [!success]- Answer
> **A.** The posterior is intractable; both VI (deterministic optimization) and Gibbs (sampling) are standard.

**15.** Increasing the Dirichlet $\alpha$ on document-topic mixtures encourages:
- A. Documents to use *more* topics in roughly equal proportions
- B. Documents to be assigned a single topic
- C. Topics to disappear
- D. Sparser documents

> [!success]- Answer
> **A.** Larger $\alpha$ → smoother mixtures; smaller $\alpha$ → each document concentrates on a few topics.

**16.** A common failure mode of vanilla LDA is:
- A. Topics that conflate semantically distinct senses of polysemous words
- B. Inability to handle long documents
- C. Producing only one topic
- D. Failing on numeric data

> [!success]- Answer
> **A.** Bag-of-words assumption ignores context; *bank* (river/finance) lands in whichever topic dominates that document.

**17.** Compared to k-means clustering of TF–IDF vectors, LDA:
- A. Allows soft, mixed-membership: a document can belong partly to multiple topics
- B. Is hard-clustering only
- C. Uses Euclidean distance
- D. Requires labels

> [!success]- Answer
> **A.** Mixed-membership is one of LDA's defining advantages — documents are mixtures, not single-cluster assignments.

**18.** The "bag of words" assumption in LDA means:
- A. Word order within documents is ignored when computing the likelihood
- B. The vocabulary is small
- C. There are no stopwords
- D. Documents are sentences

> [!success]- Answer
> **A.** This is how the multinomial likelihood is justified — the same modelling cost-saving as in NB.

**19.** Choosing the number of topics K in LDA is typically done via:
- A. Held-out perplexity, topic coherence metrics, or hierarchical priors that infer K
- B. Always K = vocabulary size
- C. Fixing K = number of documents
- D. Uniformly random

> [!success]- Answer
> **A.** No automatic ground truth; coherence (e.g., NPMI on top words) and held-out likelihood are the standard tools.

**20.** Why might LSA still be preferred over LDA in some IR settings?
- A. LSA is fast, deterministic, and often a strong unsupervised baseline for retrieval; LDA shines when interpretability of topics is the goal
- B. LDA is broken
- C. LSA is generative
- D. LSA has more parameters

> [!success]- Answer
> **A.** Use the right tool: LSA for cheap latent-semantic similarity; LDA for human-readable thematic structure.

**21.** A practitioner sees a topic with top words *{the, and, of, to, a}*. The cleanest fix is:
- A. Strip stopwords before training, or use a word-frequency-aware prior
- B. Increase K
- C. Decrease K
- D. Switch to LSA

> [!success]- Answer
> **A.** High-frequency function words can dominate topics if not filtered or downweighted.

**22.** The deepest contrast between LSA and LDA is:
- A. LSA is geometric (linear algebra on counts); LDA is generative (probabilistic story for how words appear)
- B. LSA is supervised
- C. LDA does not use words
- D. LSA produces probabilities

> [!success]- Answer
> **A.** This is the conceptual leap from VSM-era methods to Bayesian topic modelling.
