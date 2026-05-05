**Tags:** #nlp #vector-space-models #distributional-semantics #information-retrieval  
**Related:** [[NLP Fundamentals]] · [[Information Retrieval]] · [[Vector Databases]] · [[Embeddings]]

## Overview
This hub covers classical vector-space approaches to NLP: how text moves from discrete symbols to numeric representations, how those representations encode meaning through distributional patterns, and how weighting and factorization methods (TF–IDF, LSA) and contextual co-occurrence (HAL) improve retrieval and similarity beyond raw keyword matching.

## Knowledge Map

### 1. [[From Symbols to Spaces]]
- [[Vector Space Model (VSM)]]
- [[What “meaning” means in a vector space]]

### 2. [[Sparse Representations]]
- [[One-hot Encoding]]
- [[Bag-of-Words (BoW)]]
- [[Term–Document Matrix]]

### 3. [[Distributional Meaning]]
- [[Distributional Hypothesis]]
- [[Words vs Documents as Vectors]]

### 4. [[Geometric View of Meaning]]
- [[Cosine Similarity]]
- [[Set Similarity Coefficients]]
- [[Normalization - magnitude vs direction]]

### 5. [[Term Weighting]]
- [[Term Frequency (TF)]]
- [[Inverse Document Frequency (IDF)]]
- [[TF–IDF]]
- [[Limits of TF–IDF]]

### 6. [[Latent and Contextual Semantics]]
- [[Latent Semantic Analysis (LSA)]]
- [[HAL - Contextual Co-occurrence]]
- [[LSA vs HAL - global vs local structure]]

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** One-hot encoding of a 50k vocabulary produces vectors that are pairwise:
- A. Orthogonal — every two distinct words have cosine similarity 0
- B. Parallel
- C. Equally similar at cosine 0.5
- D. Negatively correlated

> [!success]- Answer
> **A.** Each word has exactly one 1 in a unique position; dot product across distinct words is always 0.

**2.** The Distributional Hypothesis (Firth/Harris) is the empirical claim that:
- A. Words that *occur in similar contexts* tend to have similar meanings
- B. Synonyms must be tagged manually
- C. Word order is irrelevant
- D. Stopwords carry the most information

> [!success]- Answer
> **A.** "You shall know a word by the company it keeps." This is the foundational premise that makes distributional semantics work.

**3.** Cosine similarity is preferred over raw dot product for comparing TF–IDF vectors because:
- A. It is faster
- B. It is invariant to document *length* (vector magnitude)
- C. It produces probabilities
- D. It works only for binary vectors

> [!success]- Answer
> **B.** Long documents have larger TF magnitudes; cosine normalizes by L2 norm so similarity reflects direction (topical content), not length.

**4.** IDF specifically penalizes terms that:
- A. Are short
- B. Appear in many documents
- C. Have low TF
- D. Are stopwords by definition

> [!success]- Answer
> **B.** $\log(N/df_t)$ shrinks toward 0 as a term appears in more documents — common terms are deemed less discriminative.

**5.** A query term has TF=10 in a document but appears in *every* document of the collection. Its TF–IDF score is:
- A. Maximal
- B. Approximately zero, because IDF ≈ 0
- C. Negative
- D. Undefined

> [!success]- Answer
> **B.** $\log(N/N) = 0$ — TF–IDF zeroes out terms with no discriminative power, regardless of frequency.

**6.** The Term–Document Matrix encodes which dual perspective?
- A. Rows = words (word vectors); columns = documents (document vectors)
- B. Rows are always queries
- C. Rows = synonyms; columns = antonyms
- D. Rows and columns must be equal in length

> [!success]- Answer
> **A.** Reading rows gives word distributions across documents; reading columns gives document distributions across the vocabulary — same matrix, two semantic views.

**7.** Bag-of-Words (BoW) discards which feature of language?
- A. Vocabulary
- B. Word order and syntactic structure
- C. Term frequency
- D. Document boundaries

> [!success]- Answer
> **B.** BoW retains counts but treats *"dog bites man"* and *"man bites dog"* as identical.

**8.** LSA reduces the term–document matrix via SVD primarily to:
- A. Speed up matrix multiplication
- B. Discover latent semantic dimensions and mitigate synonymy/polysemy
- C. Compress images
- D. Compute IDF analytically

> [!success]- Answer
> **B.** Truncated SVD projects sparse high-dimensional counts into a low-rank space where related-but-not-identical terms cluster.

**9.** A central limitation of TF–IDF is:
- A. It is too computationally expensive for small corpora
- B. It treats words as discrete symbols — synonyms remain distant; polysemes remain conflated
- C. It cannot handle term frequency
- D. It requires labeled data

> [!success]- Answer
> **B.** TF–IDF is still a sparse one-hot-like representation: *car* and *automobile* are orthogonal; *bank* (river) and *bank* (finance) share a vector.

**10.** HAL (Hyperspace Analogue to Language) differs from a term–document matrix because it:
- A. Uses a *word × word* co-occurrence matrix with a sliding window
- B. Stores TF–IDF directly
- C. Is supervised
- D. Operates on sentences only

> [!success]- Answer
> **A.** HAL captures *local* co-occurrence within a window; the term-document matrix captures *global* document-level distribution.

**11.** LSA and HAL contrast on which axis?
- A. Sparse vs dense storage
- B. Global document-level structure vs local windowed co-occurrence
- C. Supervised vs unsupervised
- D. English vs multilingual

> [!success]- Answer
> **B.** LSA aggregates over whole documents; HAL aggregates over a moving context window — different notions of "context."

**12.** Two short documents share *all* their words but in different orders. Their cosine similarity in BoW space is:
- A. 0
- B. 1
- C. 0.5
- D. Depends on word length

> [!success]- Answer
> **B.** BoW ignores order; identical word sets give identical vectors and cosine = 1.

**13.** Why is L2 normalization equivalent to projecting vectors onto the unit sphere?
- A. Because the L2 norm becomes 1, fixing magnitude
- B. Because dot products vanish
- C. Because dimensions become orthogonal
- D. Because the origin is removed

> [!success]- Answer
> **A.** Dividing by ||v|| forces ||v||=1; cosine similarity then equals the dot product on this sphere.

**14.** Jaccard similarity differs from cosine similarity by:
- A. Operating on sets, not vectors, and ignoring frequency
- B. Being signed
- C. Requiring SVD
- D. Producing values outside [0,1]

> [!success]- Answer
> **A.** Jaccard = |A∩B| / |A∪B| — purely set-theoretic, frequency-agnostic.

**15.** A term with high TF in only one document and low DF receives:
- A. Low TF–IDF
- B. High TF–IDF — the canonical signature of a discriminative term
- C. Negative TF–IDF
- D. NaN

> [!success]- Answer
> **B.** TF and IDF both push the score up; this is the prototypical "topic-signal" term.

**16.** Why does increasing vocabulary size *increase* sparsity in BoW representations?
- A. Each document still uses only a tiny subset of the vocabulary, leaving most entries 0
- B. Because IDF decreases
- C. Because cosine similarity rises
- D. Because tokens become longer

> [!success]- Answer
> **A.** The dimensionality grows but a single document touches only a few hundred unique words, so the fraction of nonzeros falls.

**17.** Replacing a Term–Document Matrix with its truncated SVD approximation changes individual entries because:
- A. The low-rank reconstruction is *not* exact — values shift toward latent-component averages
- B. SVD scales counts up
- C. SVD is supervised
- D. SVD eliminates negative numbers

> [!success]- Answer
> **A.** Truncation discards small singular values; reconstruction smears information across related terms/documents — that's what makes synonymy collapse.

**18.** Which scenario is *least* well handled by classical VSMs?
- A. Topic-level retrieval on a static corpus
- B. Resolving polysemy in context (e.g., *bank* in a sentence)
- C. Computing cosine similarity
- D. Computing TF–IDF

> [!success]- Answer
> **B.** Polysemy needs *contextual* embeddings (Transformers); a single static vector for *bank* cannot disambiguate.

**19.** A search engine using only TF (no IDF) ranks the term *the* very high in relevance to almost any query. The cleanest fix is:
- A. Disable cosine similarity
- B. Apply IDF or remove stopwords so common terms are downweighted
- C. Use one-hot encoding instead of counts
- D. Use unigrams only

> [!success]- Answer
> **B.** This is exactly the failure mode IDF was designed to correct.

**20.** Two documents have identical TF–IDF vectors. We can conclude:
- A. They have identical wording and term distributions over the corpus
- B. Their topics are weakly related
- C. They were written by the same author
- D. They are translations of each other

> [!success]- Answer
> **A.** TF–IDF is deterministic; identical vectors imply identical term frequencies and document-frequency context — usually identical text.

**21.** A *word vector* extracted from the term–document matrix encodes:
- A. The distribution of documents in which the word appears
- B. The word's grammatical role
- C. The word's pronunciation
- D. The word's morphology

> [!success]- Answer
> **A.** Reading a row of the matrix gives a fingerprint of the word over the document collection — a distributional vector.

**22.** Why does normalization matter when comparing a *short* query vector to *long* document vectors?
- A. It doesn't — dot product is fine
- B. Without normalization, longer documents dominate by magnitude regardless of topical match
- C. It removes IDF
- D. It eliminates the need for cosine

> [!success]- Answer
> **B.** Magnitude correlates with length; cosine (or L2-normalized dot product) isolates direction, which is what matters for relevance.
