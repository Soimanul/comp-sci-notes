**Tags:** #topic #hub #nlp
**Related:** [[Natural Language Processing]], [[TF–IDF]]

## Overview
Information Retrieval (IR) is the problem of selecting (and ranking) relevant information from a large collection of documents (corpus) based on a user query. 

Unlike tasks that aim to "understand" language, IR is fundamentally an ordering problem where documents are compared and ranked based on measurable statistical criteria.

## Knowledge Map
### 1. Concepts
- [[Information Retrieval vs Information Extraction]]
- [[Statistical Relevance]]

### 2. Mechanisms
- [[Relevance Feedback]]
- [[TF–IDF]]
- [[Cosine Similarity]]

### 3. Constraints
- [[Limits of Statistical Relevance]]

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** The cleanest single distinction between Information Retrieval and Information Extraction is:
- A. IR ranks documents by relevance to a query; IE pulls structured facts (entities, relations) out of text
- B. IR is supervised; IE is unsupervised
- C. IR uses neural networks; IE uses regex
- D. IR is older

> [!success]- Answer
> **A.** Different goals: IR finds *which* documents matter; IE finds *what facts* are inside them.

**2.** "Statistical relevance" in IR rests on which assumption?
- A. The query and document share a discoverable distributional signal — vocabulary overlap, term importance, etc.
- B. The query is grammatical
- C. The corpus is sorted alphabetically
- D. Documents are equal length

> [!success]- Answer
> **A.** Classical IR scores relevance from word-statistics shared between query and document; meaning is approximated by surface co-occurrence.

**3.** A user submits the query *"jaguar"* expecting car results. The classical IR system returns mostly animal pages. This failure is best categorized as:
- A. A precision/recall imbalance
- B. The vocabulary mismatch / polysemy problem — IR has no contextual disambiguation
- C. A tokenization bug
- D. A missing IDF

> [!success]- Answer
> **B.** Word-level IR cannot disambiguate senses without context; this is exactly what dense retrieval and contextual embeddings address.

**4.** Rocchio-style relevance feedback updates the query vector by:
- A. Re-tokenizing the query
- B. Moving toward the centroid of relevant documents and away from the centroid of non-relevant ones
- C. Increasing TF for stopwords
- D. Removing IDF

> [!success]- Answer
> **B.** Rocchio's update: $q' = \alpha q + \beta \bar{D}_R - \gamma \bar{D}_{NR}$ — pulls the query toward "good" documents, away from "bad" ones.

**5.** Pseudo-relevance feedback differs from explicit relevance feedback in that:
- A. It assumes the top-k results are relevant without user confirmation
- B. It uses TF only
- C. It requires no documents
- D. It is supervised

> [!success]- Answer
> **A.** Cheap and automatic, but inherits errors when the top-k aren't actually relevant — *query drift*.

**6.** A central limit of statistical relevance is:
- A. It is too slow
- B. Surface-level term matching cannot capture paraphrase, synonymy, or implication
- C. It cannot use TF–IDF
- D. It produces only binary scores

> [!success]- Answer
> **B.** *"How to repair a flat tire"* and *"fixing a punctured wheel"* share little vocabulary; classical IR ranks them as unrelated.

**7.** Why does TF–IDF underperform on *short* queries against *long* documents without normalization?
- A. Short queries have low entropy
- B. Document length inflates TF magnitudes; without cosine/L2 normalization longer documents dominate
- C. Short queries lack IDF
- D. Long documents have no idf

> [!success]- Answer
> **B.** Length bias is the cleanest single failure mode normalization fixes.

**8.** A query expansion technique adds *synonyms* of query terms before retrieval to address:
- A. The vocabulary mismatch problem
- B. Tokenization errors
- C. Backpropagation failure
- D. The Chinese Room

> [!success]- Answer
> **A.** Expanding *"car"* to *{car, automobile, vehicle}* increases the chance of matching a document that uses different surface forms for the same concept.

**9.** Which scenario is *least* well served by classical TF–IDF retrieval?
- A. Searching legal precedents by citation overlap
- B. Answering a natural-language question whose phrasing differs entirely from the documents that contain the answer
- C. Searching code repositories by exact identifier
- D. Searching news headlines by keyword

> [!success]- Answer
> **B.** This is why dense/neural retrievers (e.g., DPR) replaced TF–IDF for QA — they match on meaning, not strings.

**10.** Precision and recall trade off because:
- A. They are different definitions of accuracy
- B. Returning more documents tends to raise recall and lower precision
- C. They both equal F1
- D. They are uncorrelated

> [!success]- Answer
> **B.** Cast a wider net: catch more true positives (recall up), but also more false positives (precision down).

**11.** A search engine retrieves 100 documents; 30 are relevant. The total relevant in the corpus is 60. Recall is:
- A. 0.30
- B. 0.50 (30/60)
- C. 0.60
- D. 1.00

> [!success]- Answer
> **B.** Recall = retrieved-and-relevant / total-relevant = 30/60 = 0.5.

**12.** The *binary independence model* in IR assumes:
- A. Term occurrences in documents are independent given relevance — a strong simplifying assumption
- B. Documents are independent of queries
- C. Words are interchangeable
- D. Relevance is unobservable

> [!success]- Answer
> **A.** Like Naïve Bayes for IR — wrong but useful.

**13.** Document length normalization is *not* needed when:
- A. All documents are roughly the same length, e.g., tweets in a fixed-length corpus
- B. The query is long
- C. TF is high
- D. IDF is zero

> [!success]- Answer
> **A.** Length bias only matters when documents differ substantially in length.

**14.** BM25 improves on raw TF–IDF mainly by:
- A. Adding non-linear TF saturation and tuned length normalization
- B. Removing IDF
- C. Using softmax
- D. Computing cross-entropy

> [!success]- Answer
> **A.** BM25 caps the marginal benefit of additional term occurrences and adjusts for length via tunable *k1* and *b* parameters.

**15.** Why is "bag-of-words" a *natural* representation for IR even though it is poor for understanding?
- A. IR cares about coarse topical match across documents, not sentence-level meaning
- B. It is faster
- C. It is supervised
- D. It uses CFGs

> [!success]- Answer
> **A.** BoW is a strong baseline for retrieval because topical similarity at the document level is robust to word order — a coincidence IR exploits.

**16.** Inverted indices speed up retrieval by:
- A. Mapping each term to a posting list of documents containing it, so query evaluation touches only relevant documents
- B. Sorting documents alphabetically
- C. Caching embeddings
- D. Replacing TF with IDF

> [!success]- Answer
> **A.** This is the structural reason classical IR scales to billions of documents on commodity hardware.

**17.** A user query and a document are both represented as TF–IDF vectors. Cosine similarity returning 1.0 means:
- A. They are identical strings
- B. Their *direction* in vector space is identical (proportional term distributions); they need not be identical strings
- C. They have identical document length
- D. The query is irrelevant

> [!success]- Answer
> **B.** Cosine ignores magnitude; a short query and long document with proportional term frequencies can score 1.0.

**18.** Why does relevance feedback *fail* if too few relevant examples are provided?
- A. The centroid estimate of "relevant" is noisy and the updated query drifts toward random terms
- B. TF goes to zero
- C. The corpus shrinks
- D. IDF is undefined

> [!success]- Answer
> **A.** Few relevant docs → unreliable centroid → query drift away from the user's true intent.

**19.** Which evaluation metric is *most appropriate* for ranking quality (not just set membership)?
- A. Precision@k or nDCG, which incorporate rank position
- B. Plain accuracy
- C. Total token count
- D. Vocabulary size

> [!success]- Answer
> **A.** Set-membership metrics ignore order; nDCG/Precision@k credit highly-ranked relevant documents more.

**20.** Dense retrieval (BERT-based bi-encoders) addresses which IR weakness directly?
- A. Throughput
- B. The vocabulary mismatch problem — encoding query and document into a shared semantic space lets paraphrases match
- C. Storage cost
- D. Query parsing

> [!success]- Answer
> **B.** Dense vectors encode meaning; surface-form mismatch no longer blocks retrieval.

**21.** A search system that perfectly matches *string* but misses *intent* fails which dimension?
- A. Recall on semantic matches — high precision on lexical, low recall on conceptual
- B. Throughput
- C. Latency
- D. Indexing

> [!success]- Answer
> **A.** Conceptually relevant documents that use different words go un-retrieved; this is *semantic recall*.

**22.** The "limits of statistical relevance" argument essentially says:
- A. Word statistics alone cannot capture intent, world knowledge, or compositional meaning — there is a ceiling without semantic representations
- B. Statistics don't work
- C. IR is too slow
- D. IDF is wrong

> [!success]- Answer
> **A.** This is the motivation for semantic search and contextual embeddings: hit the ceiling of bag-of-words and bring meaning into the retriever.