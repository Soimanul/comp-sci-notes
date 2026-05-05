**Tags:** #nlp #python #libraries #pipelines #symbolic #statistical  
**Related:** [[Advanced NLP Concepts]] · [[Information Retrieval]] · [[Vector Space Model (VSM)]]

## Overview
This hub links the symbolic foundations of NLP (formal grammars and rule-based structure) to the statistical shift toward usage-based approximations, then ground those tradeoffs in practical Python tooling. It frames NLP libraries as “assumption bundles” that encode representations, pipelines, and defaults, and it positions NLTK, spaCy, Gensim, and pretrained-model interfaces as concrete implementations of different theoretical compromises.

## Knowledge Map

### 1. [[Two Ways of Thinking About Language]]
- [[Symbolic view of language]]
- [[Statistical view of language]]
- [[Cost of explicit structure]]

### 2. [[Formal Language Theory]]
- [[Chomsky and formal language theory]]
- [[Context-free grammar - CFG]]
- [[CFG derivation example]]

### 3. [[Semantic Gap and Meaning Representation]]
- [[Semantic gap]]
- [[Abstract Meaning Representation - AMR]]
- [[AMR example - active vs passive equivalence]]

### 4. [[NLP Libraries and Pipelines]]
- [[NLP libraries encode assumptions]]
- [[Common NLP pipeline stages]]
- [[Library tradeoffs - control vs robustness]]

### 5. [[Python NLP Tooling Landscape]]
- [[NLTK]]
- [[spaCy]]
- [[Gensim]]
- [[Pretrained models - Transformers]]

### 6. [[Practice Assignment - Vector Space Model with Libraries]]

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** A team chooses a Context-Free Grammar to parse user queries for a banking app. The cleanest single argument *against* this choice is:
- A. CFGs are slower than regex
- B. Real user queries contain ambiguity, ungrammaticality, and long-tail constructions that no hand-written CFG can fully cover
- C. CFGs cannot recognize parentheses
- D. CFGs are not Turing-complete

> [!success]- Answer
> **B.** This is the symbolic-era brittleness problem; the cost of explicit structure is engineering time and inevitable coverage gaps.

**2.** Which is a strict capability boundary of CFGs?
- A. They cannot model recursive structure
- B. They cannot capture cross-serial dependencies (mildly context-sensitive phenomena like Swiss-German verb cluster)
- C. They cannot describe arithmetic expressions
- D. They require neural training

> [!success]- Answer
> **B.** This is the classic argument that natural language is not strictly context-free; CFGs capture nesting but not crossing dependencies.

**3.** The "semantic gap" refers to:
- A. The gap between training and test loss
- B. The mismatch between surface form and the underlying meaning we want a representation to expose
- C. The latency between tokens
- D. The vocabulary gap between languages

> [!success]- Answer
> **B.** Two utterances with different surface forms can mean the same thing; the gap is what AMR-style representations try to close.

**4.** Active and passive paraphrases (*"The cat chased the mouse" / "The mouse was chased by the cat"*) collapse to the same AMR because AMR encodes:
- A. Token sequences
- B. Predicate–argument structure (who did what to whom), independent of surface order
- C. POS tags only
- D. Part-of-speech bigrams

> [!success]- Answer
> **B.** AMR is a rooted, directed graph of semantic roles — voice alternations don't change the underlying agent/patient relations.

**5.** spaCy is *opinionated* in a way NLTK is not. The most consequential design difference is:
- A. spaCy ships production-grade default pipelines with prebuilt models; NLTK is a teaching toolkit of pluggable components
- B. spaCy is symbolic; NLTK is neural
- C. spaCy uses Python; NLTK uses Java
- D. spaCy lacks tokenizers

> [!success]- Answer
> **A.** Pipeline philosophy differs: spaCy = batteries-included production; NLTK = research/education with finer-grained, slower defaults.

**6.** Gensim's primary domain is:
- A. Dependency parsing
- B. Topic modelling and unsupervised vector-space methods (LSA, LDA, Word2Vec)
- C. Speech recognition
- D. Image captioning

> [!success]- Answer
> **B.** Gensim was built around scalable streaming algorithms for topic models and word embeddings.

**7.** The claim "NLP libraries encode assumptions" is best illustrated by:
- A. Two libraries returning identical token sequences
- B. spaCy's default tokenizer splitting *don't* into *do* + *n't*, while NLTK's word_tokenize may keep *don't* whole
- C. Both libraries depending on the same C compiler
- D. Identical handling of punctuation across all libraries

> [!success]- Answer
> **B.** Tokenization choices propagate downstream — the same input becomes different feature spaces under different libraries.

**8.** Which pipeline stage is *typically* skipped in modern Transformer-based pipelines compared to classical ones?
- A. Tokenization
- B. POS tagging as an explicit upstream step (Transformers learn it implicitly)
- C. Embedding
- D. Inference

> [!success]- Answer
> **B.** Pretrained Transformers fold many classical stages into representation learning; pipelines flatten.

**9.** The fundamental tradeoff between *control* (NLTK-style) and *robustness* (spaCy-style) is:
- A. Speed vs accuracy
- B. Fine-grained customization vs strong defaults that "just work" on real text
- C. Free vs paid
- D. Python vs C++

> [!success]- Answer
> **B.** Control gives you knobs; robustness gives you reliable behavior across messy real-world inputs at the cost of some flexibility.

**10.** Symbolic and statistical views of language are best framed as:
- A. Mutually exclusive paradigms
- B. Complementary lenses — symbolic accounts for compositional structure, statistical for usage frequency and ambiguity
- C. Outdated and modern
- D. Linguistic and computational

> [!success]- Answer
> **B.** Modern systems often use statistical learning to *induce* structure that approximates symbolic representations.

**11.** Which sentence is genuinely problematic for a *probabilistic* CFG but trivial for a Transformer?
- A. *"I saw the man with the telescope."* (PP-attachment ambiguity)
- B. *"The cat sat."*
- C. *"Run!"*
- D. *"Hello."*

> [!success]- Answer
> **A.** PP-attachment ambiguity requires world knowledge; PCFGs can rank parses by tree probability but lack the lexical/semantic context that a Transformer's contextual embeddings provide.

**12.** A pipeline performs: tokenize → POS tag → lemmatize → vectorize → classify. If lemmatization is omitted, what is the *most likely* downstream effect?
- A. The model becomes faster but its vocabulary fragments across inflectional variants
- B. POS tagging fails
- C. Tokenization becomes incorrect
- D. The classifier's labels change

> [!success]- Answer
> **A.** Without lemmatization, *run/ran/runs* occupy separate vocabulary slots, splitting the signal across forms.

**13.** A practitioner switches a tokenizer mid-experiment without retraining. The validity of comparing models trained before and after is:
- A. Unaffected
- B. Compromised — the input feature distribution changed, so loss numbers are not comparable
- C. Improved
- D. Always neutral

> [!success]- Answer
> **B.** Tokenization defines the input space; changing it without retraining invalidates comparisons.

**14.** Pretrained Transformers shift the engineering effort from:
- A. Inference to training
- B. Hand-crafting features and pipelines to fine-tuning and prompt design
- C. Tokenization to lemmatization
- D. POS tagging to parsing

> [!success]- Answer
> **B.** The locus of effort moved up the abstraction stack — you now adapt a general model rather than build feature pipelines from scratch.

**15.** Which library would you reach for *first* if asked to compute LSA over a 10-million-document corpus?
- A. NLTK
- B. Gensim, because of its streaming/incremental algorithms designed for corpora that don't fit in RAM
- C. spaCy
- D. PyTorch

> [!success]- Answer
> **B.** Gensim is built around online/streaming SVD and LDA — that's its niche.

**16.** A CFG derivation tree is most useful when:
- A. You need to expose explicit constituent structure for downstream rule-based reasoning
- B. You only care about classification accuracy
- C. You are doing image classification
- D. You want to estimate term frequency

> [!success]- Answer
> **A.** Trees are the natural input to compositional semantics, query parsers, and other systems that need explicit structure.

**17.** Why is the cost of explicit structure higher in NLP than, say, in compilers?
- A. Compilers don't run on Linux
- B. Programming languages are designed to be unambiguous; natural language is intrinsically ambiguous and constantly evolving
- C. Compilers do not use grammars
- D. NLP requires GPUs

> [!success]- Answer
> **B.** Engineered languages are bounded by spec; natural language is open-ended — making rule-coverage asymptotically futile.

**18.** Which library provides the *richest set of classical algorithms* (probabilistic parsers, WordNet integration, n-gram tools) at the cost of being slower?
- A. spaCy
- B. NLTK
- C. Gensim
- D. PyTorch

> [!success]- Answer
> **B.** NLTK is the textbook companion library — broad, educational, and not optimized for production throughput.

**19.** When a practitioner says "the library encodes assumptions," they mean:
- A. Default settings (tokenizer rules, sentence splitter, POS scheme) constrain how problems are framed
- B. The library has a configuration file
- C. The library is biased toward English
- D. The library uses regex

> [!success]- Answer
> **A.** The defaults are theory-laden choices; if you accept them, you inherit a particular linguistic worldview.

**20.** A Transformer pipeline would still benefit from explicit pre-tokenization for which case?
- A. Domain text with custom delimiters (DNA sequences, source code) where the default subword tokenizer behaves badly
- B. Standard English news
- C. Short queries
- D. Numeric data

> [!success]- Answer
> **A.** Domain-specific input distributions diverge from a general subword vocabulary; a custom tokenizer is often the right intervention.

**21.** The *cost of explicit structure* is paid mostly in:
- A. CPU cycles
- B. Engineer time and brittleness on long-tail input
- C. RAM
- D. Network bandwidth

> [!success]- Answer
> **B.** Hand-built grammars are expensive to write, maintain, and extend — and they fail in ways that data-driven systems don't.

**22.** A central reason to learn the symbolic perspective even when using neural tools is:
- A. To compile the model faster
- B. To reason about *what* a model should compute (predicate-argument structure, scope, coreference) — even when you let it learn *how*
- C. Symbolic always outperforms neural
- D. Neural networks cannot tokenize

> [!success]- Answer
> **B.** Symbolic theory gives you the vocabulary to specify problems and diagnose failures; neural models give you the machinery to solve them.

