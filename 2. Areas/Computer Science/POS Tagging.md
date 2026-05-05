**Tags:** #hub #nlp #pos #sequence-labelling
**Related:** [[Natural Language Processing]], [[Markov Assumption]], [[Named Entity Recognition]]

## Overview

Part-of-Speech (POS) tagging assigns a grammatical category (noun, verb, adjective, …) to each token in a sentence. It is the structural layer in the NLP pipeline that comes after tokenisation and morphological analysis and before syntactic parsing. Conceptually, POS tagging extends classifier ideas (Naïve Bayes, logistic regression) into the **structured prediction** regime, where the predictions at different positions are not independent.

> [!abstract]- TL;DR
> POS tagging is structured prediction: predict an entire tag sequence rather than independent labels. Rule-based systems collapse under ambiguity; classical statistical solutions use HMM with Viterbi decoding; modern systems use neural taggers. The conceptual machinery — conditional probabilities, smoothing, likelihood maximisation — is identical to Naïve Bayes; only the **interdependence across positions** is new.

## Knowledge Map

### 1. The Problem
- [[POS as Structured Prediction]]
- [[Limits of Rule-Based Tagging]]

### 2. Tag Sets
- [[Penn Treebank POS Tagset]]
- [[Universal POS Tags]]

### 3. Classical Probabilistic Approach
- [[HMM-Based POS Tagger]]
- [[Viterbi Algorithm]]
- [[What HMM Captures and Misses]]

### 4. Neural Approaches
- [[Neural POS Tagger]]

> [!question]- Common Exam Questions
> - Why is POS tagging a structured prediction problem and not just a classification problem?
> - State the two HMM independence assumptions and the resulting joint probability.
> - Trace Viterbi for *"They can fish"* given a small transition/emission table.
> - What does the HMM tagger explicitly fail to capture that a Transformer does not?
> - Why do rule-based taggers fail on natural language ambiguity?

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** POS tagging is a *structured* prediction problem because:
- A. The label at position $t$ depends on labels at adjacent positions; predicting them independently is suboptimal
- B. Tags are nested
- C. Tags are continuous
- D. Tags require regex

> [!success]- Answer
> **A.** Independent classification ignores tag-tag transitions (verbs follow nouns more often than verbs follow verbs); structured models exploit this.

**2.** The HMM POS tagger's two independence assumptions are:
- A. (i) tag at $t$ depends only on tag at $t{-}1$ (Markov), (ii) word at $t$ depends only on tag at $t$ (output independence)
- B. Tags are independent of words
- C. Tags are uniformly distributed
- D. Words are independent of tags

> [!success]- Answer
> **A.** These two assumptions yield the factored joint $P(\mathbf{w},\mathbf{t})=\prod P(t_i|t_{i-1})P(w_i|t_i)$.

**3.** Viterbi solves which problem?
- A. Argmax of joint probability over tag sequences in O(T·|S|²) using dynamic programming
- B. Sum over all tag sequences
- C. Sample from the posterior
- D. Train the HMM

> [!success]- Answer
> **A.** Viterbi finds the *most likely* tag sequence; the *forward* algorithm computes the marginal likelihood.

**4.** Naïve enumeration of tag sequences is intractable because:
- A. There are |S|^T sequences for T tokens — exponential in sequence length
- B. Sequences are infinite
- C. Tags repeat
- D. Words are infinite

> [!success]- Answer
> **A.** DP on a trellis collapses this to polynomial time.

**5.** The Penn Treebank tagset has roughly:
- A. 12 tags
- B. 36 tags (for English) — fine-grained morphosyntactic distinctions
- C. 100 tags
- D. 1000 tags

> [!success]- Answer
> **B.** Penn distinguishes verb forms (VBD, VBG, VBN, VBP, VBZ) and number on nouns; Universal POS uses ~17 coarser tags.

**6.** Universal POS Tags differ from Penn primarily by:
- A. Being coarser and language-agnostic — designed for cross-lingual NLP
- B. Being case-insensitive
- C. Using regex
- D. Being a superset of Penn

> [!success]- Answer
> **A.** Universal collapses Penn's fine grain so that one tagset works across many languages.

**7.** A bigram HMM emits *time* with probability $P(time|N) = 0.0005$ and $P(time|V) = 0.0001$. Without considering context, the tagger would prefer:
- A. Noun
- B. Verb
- C. Either equally
- D. Neither

> [!success]- Answer
> **A.** Higher emission probability under N. Context (transitions and surrounding words) is what makes Viterbi different from simple per-token argmax.

**8.** Smoothing in HMM emission probabilities matters most because:
- A. Without it, an unseen (word, tag) pair zeros the entire sequence probability
- B. It speeds up Viterbi
- C. It eliminates transitions
- D. It makes the model deterministic

> [!success]- Answer
> **A.** Unknown-word handling (or smoothing/backoff) is essential — same problem as in NB.

**9.** The HMM POS tagger fundamentally misses:
- A. Long-range dependencies and rich lexical context — it sees only the immediately previous tag and the current word
- B. Tokenization
- C. The vocabulary
- D. The Markov assumption

> [!success]- Answer
> **A.** First-order Markov + emission independence is exactly what neural taggers (BiLSTMs, Transformers) overcome.

**10.** A neural POS tagger with a BiLSTM over word embeddings improves on HMM mainly because:
- A. It conditions each tag prediction on the *entire* sentence representation, capturing long-range and morphological context
- B. It is faster
- C. It removes the need for tags
- D. It uses regex

> [!success]- Answer
> **A.** Bidirectional context replaces the local-Markov assumption with a learned global encoding.

**11.** Why do rule-based taggers fail on *"flies"*?
- A. The word is ambiguous (NNS or VBZ); rules without strong context cues cannot disambiguate consistently
- B. Rules are slow
- C. *flies* is OOV
- D. Rules cannot match suffixes

> [!success]- Answer
> **A.** Genuine ambiguity is the structural killer; resolution needs context, not rules alone.

**12.** What does Viterbi store at each cell of the trellis?
- A. The maximum probability of any tag sequence ending in that cell, plus a backpointer to the previous best tag
- B. The full sentence
- C. All tag sequences
- D. The vocabulary

> [!success]- Answer
> **A.** Standard DP table: max-score per (position, tag) + backpointer for trace.

**13.** The tradeoff between Penn and Universal tagsets is:
- A. Granularity vs portability — Penn captures more morphosyntax; Universal generalizes across languages with less detail
- B. Speed
- C. Accuracy only
- D. Open-source vs proprietary

> [!success]- Answer
> **A.** Choose Penn for English-rich syntax; Universal for cross-lingual or coarse tasks.

**14.** A practitioner reports their HMM tagger fails on social-media text more than on news. The cleanest single explanation is:
- A. Out-of-vocabulary words, non-standard orthography, and shifted distributions break the HMM's emission and transition statistics learned on news
- B. HMMs cannot handle short text
- C. Viterbi is wrong
- D. Tagsets do not include emoji

> [!success]- Answer
> **A.** Domain shift hits both lexical and structural assumptions.

**15.** A first-order HMM transition matrix has size:
- A. |S| × |S| where |S| is the number of tags
- B. T × T where T is sentence length
- C. |V| × |V|
- D. |V| × |S|

> [!success]- Answer
> **A.** Tag-to-tag transitions; emissions are |S| × |V|.

**16.** Why is POS tagging often modelled as a *generative* HMM rather than a discriminative model?
- A. HMMs are simpler to estimate from labeled data with closed-form MLE; CRFs (discriminative) outperform but are more complex to train
- B. Discriminative models are impossible
- C. HMMs are exact
- D. Tagging requires generation

> [!success]- Answer
> **A.** HMMs are the textbook starting point; CRFs and neural taggers are the discriminative successors that drop the independence assumptions.

**17.** A second-order HMM (trigram tagger) conditions on:
- A. The two previous tags — better local context, more parameters, more data sparsity
- B. The current word only
- C. The next two tags
- D. The vocabulary

> [!success]- Answer
> **A.** Higher order captures longer dependencies but pays in sparsity (typical n-gram tradeoff).

**18.** Why is POS tagging accuracy near 97% on news but lower on Twitter?
- A. The training distribution differs — domain shift, OOVs, and non-canonical syntax all hurt
- B. POS does not exist on Twitter
- C. Twitter is too short
- D. Twitter uses Universal tags only

> [!success]- Answer
> **A.** This is a recurring theme in NLP: in-domain wins are large; cross-domain accuracy degrades quickly.

**19.** *"They refuse to permit us to obtain the refuse permit."* — *refuse* and *permit* alternate POS within the sentence. A first-order HMM:
- A. Can disambiguate using transition probabilities (NN follows DT/PRP$ more, VB follows TO etc.)
- B. Cannot disambiguate at all
- C. Always fails
- D. Tags both as NN

> [!success]- Answer
> **A.** Transition statistics give just enough context to flip *refuse* between V and N at the right positions.

**20.** A *closed-class* word category (e.g., determiners, prepositions) is:
- A. A small, slowly-changing set of tokens — high-quality emission probabilities are easy to learn
- B. The same as nouns
- C. Rich in morphology
- D. Open to new entries

> [!success]- Answer
> **A.** Closed classes are robust signals for taggers; open classes (nouns, verbs) carry the OOV burden.

**21.** Why does a Transformer tagger typically outperform a neural BiLSTM tagger?
- A. Self-attention provides richer global context per token and benefits from massive pretraining
- B. Transformers use Viterbi
- C. BiLSTMs cannot tag
- D. Transformers are smaller

> [!success]- Answer
> **A.** Pretraining + attention are the two structural wins.

**22.** A useful mental model for the HMM POS tagger is:
- A. A path-finding problem on a tag-by-position lattice with transition and emission costs
- B. A clustering problem
- C. A regression problem
- D. A sorting problem

> [!success]- Answer
> **A.** Viterbi is shortest-path on the trellis where edges encode log-probabilities.
