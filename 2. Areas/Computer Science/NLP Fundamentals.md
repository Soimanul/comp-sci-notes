**Tags:** #topic #hub #nlp #fundamentals 
**Related:** [[History of NLP]], [[Natural Language Processing]]

## Overview
This hub covers the foundational building blocks of Natural Language Processing. It bridges the gap from raw text manipulation (Preprocessing) to probabilistic sequencing (Statistical Models) and the biological inspiration behind modern AI (Neural Networks).

## Knowledge Map
### 1. [[NLP Preprocessing]]
- [[Tokenization]]
- [[Morphemes]]
- [[Subwords]]
- [[Normalization (in NLP)]]

### 2. [[Statistical Language Models]]
- [[N-gram Model]]
- [[Markov Assumption]]

### 3. [[Neural Foundations]]
- [[McCulloch-Pitts Neuron]] (The Logic Gate)
- [[Perceptron]] (The Learner)
- [[Bias (Neural Networks)]]
- [[Activation Functions]]

### 4. [[Deep Learning Architectures]]
- [[Multilayer Perceptron]] (MLP)
- [[Feedforward Neural Network]]
- [[Backpropagation]] (The Learning Algorithm)
- [[Epoch]]

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions
> Cover yourself, pick an answer, then expand the spoiler. Aim for ≥18/22.

**1.** Whitespace tokenization on Mandarin Chinese fails for which fundamental reason?
- A. Mandarin has no morphology
- B. Mandarin orthography does not delimit words with spaces, so the tokenizer's primary cue is missing
- C. Unicode does not encode Chinese
- D. Tokenizers cannot run on RTL scripts

> [!success]- Answer
> **B.** Tokenizers built for English implicitly assume orthographic word boundaries; languages without those boundaries break the assumption.

**2.** A bigram model with no smoothing assigns probability 0 to *"the quokka jumped"* even though every word is in the vocabulary. Why?
- A. The unigram probability of *quokka* is 0
- B. The bigram *(quokka, jumped)* never occurred in training
- C. The Markov assumption was violated
- D. Backoff was disabled at the unigram level

> [!success]- Answer
> **B.** Zero training count for any required bigram zeros the entire product. This is exactly the problem smoothing was invented to fix.

**3.** The Markov assumption in an n-gram model trades:
- A. Memory for compute
- B. Tractability for an explicit, controlled approximation of context
- C. Probability for determinism
- D. Recall for precision

> [!success]- Answer
> **B.** Truncating history to *n−1* tokens makes parameter estimation tractable; the cost is paid in long-range dependencies.

**4.** Subword tokenization (BPE, WordPiece) primarily addresses which problem that pure word-level tokenization cannot?
- A. Casing
- B. Out-of-vocabulary words and morphological richness
- C. Sentence segmentation
- D. POS ambiguity

> [!success]- Answer
> **B.** Subwords decompose unseen or rare words into known fragments, eliminating the OOV cliff and giving morphologically rich languages a fairer footing.

**5.** Lowercasing as a normalization step is risky for which task?
- A. Topic modelling on news
- B. Named-entity recognition where *Apple* (company) ≠ *apple* (fruit)
- C. Spam classification
- D. Language identification

> [!success]- Answer
> **B.** NER relies on case as a signal; collapsing it destroys information the model would otherwise use.

**6.** The McCulloch–Pitts neuron differs from the perceptron in that:
- A. It uses sigmoid activation; the perceptron uses ReLU
- B. It is purely a logical/threshold device with fixed weights; the perceptron *learns* weights from data
- C. It has more layers
- D. It uses backpropagation

> [!success]- Answer
> **B.** McCulloch–Pitts (1943) modeled the neuron as a logic gate. Rosenblatt's perceptron (1958) added a learning rule for the weights.

**7.** Why does an XOR function break a single-layer perceptron?
- A. XOR has too many inputs
- B. XOR is not linearly separable in input space
- C. XOR requires a softmax output
- D. The perceptron cannot use bias

> [!success]- Answer
> **B.** Minsky and Papert's 1969 result; you need at least one hidden layer to bend the decision surface around the non-linear class boundary.

**8.** Removing the bias term from a neuron is equivalent to:
- A. Forcing the activation function to pass through the origin
- B. Constraining the decision boundary to pass through the origin of input space
- C. Disabling backpropagation
- D. Making the neuron stateless

> [!success]- Answer
> **B.** Without bias, the hyperplane *w·x = 0* is forced through 0 — many real datasets cannot be separated under that constraint.

**9.** Which activation function is chosen specifically because its derivative is cheap and it does not saturate for positive inputs?
- A. Sigmoid
- B. Tanh
- C. ReLU
- D. Softmax

> [!success]- Answer
> **C.** ReLU's derivative is 0 or 1; gradients flow undamped on the positive side, mitigating vanishing gradients in deep stacks.

**10.** Backpropagation is best described as:
- A. A second-order optimization method
- B. The chain rule applied recursively to a computational graph to propagate gradients backwards
- C. A heuristic for initializing weights
- D. A regularization technique

> [!success]- Answer
> **B.** Backprop is *not* an optimizer (SGD/Adam are); it is the gradient-computation step that those optimizers consume.

**11.** Increasing epochs without other changes typically risks:
- A. Underfitting
- B. Overfitting and memorization of the training set
- C. Vanishing gradients
- D. Tokenization errors

> [!success]- Answer
> **B.** Repeated passes over the same data drive training loss down but eventually start fitting noise — validation loss diverges from training loss.

**12.** A character-level model and a word-level model are trained on the same corpus. The character model has:
- A. A much larger vocabulary
- B. A much smaller vocabulary but longer sequences
- C. Identical sequence lengths
- D. No notion of vocabulary

> [!success]- Answer
> **B.** Vocab shrinks to a few hundred symbols; sequences inflate by ~5× because each word becomes multiple tokens.

**13.** Stemming and lemmatization both reduce inflection. The key difference is:
- A. Lemmatization is faster
- B. Stemming uses heuristic suffix-stripping; lemmatization returns a valid dictionary form using POS and morphology
- C. Stemming requires a parser
- D. Lemmatization is language-agnostic

> [!success]- Answer
> **B.** Stemmers (e.g., Porter) chop endings algorithmically — fast but produce non-words like *univers*. Lemmatizers consult a lexicon and POS to return *university*.

**14.** A trigram model's perplexity on held-out text is *higher* than its bigram counterpart. The most likely cause is:
- A. The trigram model is overfitting / data sparsity at order 3 hurts more than longer context helps
- B. The Markov assumption fails at order 2
- C. Smoothing was over-applied to the bigram
- D. Trigrams cannot model English

> [!success]- Answer
> **A.** Higher-order n-grams have exponentially more parameters; without enough data and proper smoothing, sparsity dominates.

**15.** A feedforward network with one hidden layer and a non-linear activation can, in principle, approximate:
- A. Only linear functions
- B. Any continuous function on a compact domain (universal approximation)
- C. Only Boolean functions
- D. Only convex functions

> [!success]- Answer
> **B.** Cybenko/Hornik's universal-approximation theorem — but "can in principle" hides the catch: width and data needed may be impractical.

**16.** Which preprocessing step would *most* harm a sentiment classifier?
- A. Removing HTML tags
- B. Removing all punctuation, including '!' and '?'
- C. Lowercasing
- D. Stripping leading whitespace

> [!success]- Answer
> **B.** Exclamation and question marks carry strong affect signals; removing them collapses *"Great!!!"* and *"Great"* into the same token.

**17.** In SGD with mini-batches, an *epoch* is defined as:
- A. One forward pass
- B. One full sweep through the entire training set
- C. The point at which validation loss plateaus
- D. The number of mini-batches per second

> [!success]- Answer
> **B.** One epoch = one complete iteration over all training examples, regardless of batch size.

**18.** Which fact most strongly motivates using subwords in a multilingual model?
- A. They reduce GPU memory
- B. They provide a shared symbol space across scripts and reduce OOV across languages
- C. They are case-insensitive
- D. They eliminate the need for embeddings

> [!success]- Answer
> **B.** A single subword vocabulary spans many languages, enabling cross-lingual transfer that pure word-level vocabularies cannot.

**19.** Why does the perceptron learning rule converge only on linearly separable data?
- A. It uses momentum
- B. The proof relies on the existence of a separating hyperplane with positive margin; without one, updates oscillate
- C. The bias term diverges
- D. The activation is non-monotonic

> [!success]- Answer
> **B.** The Perceptron Convergence Theorem (Novikoff) bounds updates by 1/γ² where γ is the margin — no margin, no bound.

**20.** The principal practical advantage of statistical LMs over symbolic grammars for sequence modelling is:
- A. They handle ambiguity by ranking hypotheses with probabilities
- B. They do not require any data
- C. They produce parse trees
- D. They guarantee grammaticality

> [!success]- Answer
> **A.** Probabilities give a principled way to choose among competing parses or continuations; symbolic systems often had no tiebreaker.

**21.** A neural FFN trained with backprop will fail to learn if all weights are initialized to the *same* constant. Why?
- A. The loss explodes
- B. Symmetry: every neuron in a layer computes the same gradient and remains identical forever
- C. Bias terms saturate
- D. ReLU dies

> [!success]- Answer
> **B.** Symmetry breaking requires non-equal initial weights; otherwise the hidden units are functionally a single unit.

**22.** Among preprocessing, statistical models, and neural foundations, which dependency is real?
- A. Neural models eliminate the need for tokenization
- B. Statistical n-gram models still require some form of tokenization to define their unit of probability
- C. Tokenization presupposes a neural network
- D. Backpropagation requires symbolic grammar

> [!success]- Answer
> **B.** "n-gram of *what*?" — tokens. Tokenization defines the random variable; without it, the LM has no unit to assign probability to.