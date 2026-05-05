**Tags:** #topic #hub #nlp
**Related:** [[Natural Language Processing]], [[Text Classification]]

## Overview
Naïve Bayes is a probabilistic, generative classifier based on [[Bayes' Theorem]]. It is often referred to as the "simplest classifier" because it assumes that all features (words) are conditionally independent given the class, which greatly simplifies the computation required for text classification tasks.

## Knowledge Map
### 1. Foundations
- [[Bayes' Theorem]]
- [[Text Classification]]

### 2. The Model
- [[Naïve Bayes Independence Assumption]]
- [[Log-Probabilities in Naïve Bayes]]
- [[Laplace Smoothing]]

### 3. Evaluation
- [[Evaluation Metrics for Classifiers]]
- [[Confusion Matrix]]

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** Naïve Bayes is called *generative* because it models:
- A. The conditional $P(y \mid x)$ directly
- B. The joint distribution via $P(x \mid y) \cdot P(y)$ — and can in principle generate samples
- C. Only the marginal $P(x)$
- D. The decision boundary

> [!success]- Answer
> **B.** Generative classifiers learn class-conditional distributions; this contrasts with discriminative models like logistic regression that go straight for $P(y|x)$.

**2.** The "naïve" assumption is that:
- A. Features are independent given the class
- B. Classes are equally likely
- C. The vocabulary is small
- D. The classifier ignores the prior

> [!success]- Answer
> **A.** Conditional independence given the class — known to be false for language but useful as a simplification.

**3.** Without smoothing, a single unseen word in the test document causes:
- A. The class posterior to become 0 because one factor in the product is 0
- B. The classifier to default to the prior
- C. Higher accuracy
- D. A negative probability

> [!success]- Answer
> **A.** One zero kills the entire product — Laplace/Lidstone smoothing exists exactly to prevent this.

**4.** Add-one (Laplace) smoothing for $P(w|c)$ replaces $\frac{count(w,c)}{count(c)}$ with:
- A. $\frac{count(w,c)+1}{count(c)+|V|}$ where |V| is the vocabulary size
- B. $\frac{count(w,c)}{count(c)+1}$
- C. $\frac{count(w,c)+1}{count(c)}$
- D. $\frac{1}{count(c)+|V|}$

> [!success]- Answer
> **A.** Numerator gets +1; denominator gets +|V| so the conditional remains a valid probability distribution.

**5.** Naïve Bayes works in *log space* primarily to avoid:
- A. Negative numbers
- B. Underflow when multiplying many small probabilities
- C. Slow training
- D. Smoothing

> [!success]- Answer
> **B.** Products of many sub-1 floats underflow; converting to a sum of log-probabilities is numerically stable.

**6.** A classifier achieves 99% accuracy on a dataset where 99% of examples are negative. The most likely interpretation is:
- A. The classifier is excellent
- B. Accuracy is misleading — the model may be predicting "negative" for everything; check precision/recall on the positive class
- C. Naïve Bayes always achieves 99%
- D. The data is noise-free

> [!success]- Answer
> **B.** Class imbalance breaks accuracy as a metric; F1, recall, and AUROC are more honest.

**7.** Recall is the answer to which question?
- A. *Of the items I predicted positive, how many really are positive?*
- B. *Of the truly positive items, how many did I retrieve?*
- C. *What fraction of all predictions are correct?*
- D. *What is the accuracy of negative predictions?*

> [!success]- Answer
> **B.** Recall = TP / (TP + FN) — coverage of the positive class.

**8.** Precision is the answer to which question?
- A. *Of the items I predicted positive, how many really are positive?*
- B. *Of the truly positive items, how many did I retrieve?*
- C. *What fraction of all predictions are correct?*
- D. *What is the accuracy of the prior?*

> [!success]- Answer
> **A.** Precision = TP / (TP + FP).

**9.** Why is the F1 score the harmonic mean rather than the arithmetic mean of precision and recall?
- A. Harmonic means penalize the lower of the two more heavily — both must be reasonable for F1 to be high
- B. To match a Gaussian
- C. Tradition only
- D. To be in [0, 0.5]

> [!success]- Answer
> **A.** Harmonic mean punishes imbalance: 0 precision drives F1 to 0 even if recall is 1.

**10.** Multinomial Naïve Bayes differs from Bernoulli Naïve Bayes in that:
- A. Multinomial uses term frequencies; Bernoulli uses binary presence/absence
- B. Multinomial is unsupervised
- C. Bernoulli is for continuous features
- D. They are identical

> [!success]- Answer
> **A.** Multinomial conditions on counts; Bernoulli on a binary "did the word occur?" feature.

**11.** The *prior* $P(c)$ is typically estimated from training data as:
- A. The fraction of training documents in class c
- B. Always uniform
- C. The TF–IDF of the class
- D. 1/|V|

> [!success]- Answer
> **A.** Empirical class frequency is the maximum-likelihood estimate of the prior.

**12.** Even though the conditional independence assumption is wrong, NB often performs well in text classification because:
- A. Probability *estimates* are biased but the *argmax* over classes is often still correct
- B. Independence holds for words
- C. Smoothing fixes everything
- D. Text is low-dimensional

> [!success]- Answer
> **A.** This is Domingos & Pazzani's classic result: NB's calibration is poor but its decisions can still be on the right side of the boundary.

**13.** A spam classifier trained with Naïve Bayes systematically scores legitimate financial emails as spam. The most likely cause is:
- A. Words like *"loan"*, *"investment"* have high $P(w|spam)$ in the training set; without enough legitimate finance examples, the prior pulls predictions toward spam
- B. Smoothing is too aggressive
- C. The model is overparameterized
- D. NB cannot represent finance terms

> [!success]- Answer
> **A.** Distributional skew in training data is the typical culprit; NB has no contextual disambiguation.

**14.** The decision rule is $\arg\max_c P(c) \prod_i P(w_i|c)$. Why is the *normalizer* $P(x)$ ignored?
- A. It is the same for every class and drops out of the argmax
- B. It is always 1
- C. It is unknown and must be estimated separately
- D. It varies with the prior only

> [!success]- Answer
> **A.** $P(x)$ doesn't depend on $c$; it cancels in the comparison.

**15.** A confusion matrix's *off-diagonal* entries indicate:
- A. Correct predictions
- B. Errors — either false positives (column) or false negatives (row), depending on layout
- C. The prior
- D. Smoothing parameters

> [!success]- Answer
> **B.** Diagonals are correct counts; off-diagonals partition errors by direction.

**16.** Why is *accuracy* especially misleading on the IMDB sentiment task with class-balanced data and *not* on a 99/1 imbalanced spam corpus?
- A. Accuracy aligns with intent on balanced data; on imbalanced data the trivial classifier wins on accuracy alone
- B. Accuracy is undefined on balanced data
- C. Sentiment cannot be measured
- D. Spam is binary

> [!success]- Answer
> **A.** Balance removes the imbalance pathology; accuracy becomes a fair scorer.

**17.** A weakness of Multinomial NB on long documents is:
- A. Highly frequent terms dominate the log-product even after IDF
- B. It cannot handle short documents
- C. It requires Laplace smoothing
- D. It produces only one class

> [!success]- Answer
> **A.** Length-driven bias is real; using TF transformations or length-normalized features helps.

**18.** Why does Bernoulli NB sometimes outperform Multinomial NB on *short texts* like tweets?
- A. Presence/absence is more informative than count when documents are too short for counts to vary meaningfully
- B. Bernoulli is faster
- C. Tweets violate independence
- D. Multinomial cannot tokenize tweets

> [!success]- Answer
> **A.** When most words occur 0 or 1 times, the binary representation captures essentially the same signal with less noise.

**19.** Macro-averaged F1 differs from micro-averaged F1 in that:
- A. Macro averages F1 *per class*; micro pools all TP/FP/FN before computing one F1 — micro is dominated by the majority class
- B. Macro is faster
- C. Micro ignores class
- D. They are identical

> [!success]- Answer
> **A.** Use macro for class-balanced evaluation; use micro when overall throughput matters.

**20.** A Naïve Bayes classifier's *log-likelihood* of a document under class c equals:
- A. $\log P(c) + \sum_i \log P(w_i|c)$
- B. $\log P(c) \cdot \sum_i P(w_i|c)$
- C. $\sum_i \log P(c|w_i)$
- D. $P(c) \cdot \prod_i P(w_i|c)$

> [!success]- Answer
> **A.** Log-prior plus sum of log-conditionals — the standard scoring function used in implementations.

**21.** Smoothing introduces bias to reduce variance. The *Lidstone* parameter $\alpha$ should be chosen by:
- A. Validation set performance
- B. Setting it to 0 always
- C. Setting it to |V|
- D. Setting it to the class prior

> [!success]- Answer
> **A.** Treat $\alpha$ as a hyperparameter; tune via held-out data.

**22.** The deepest reason NB underperforms BERT on sentiment is:
- A. Slower inference
- B. NB has no contextual representation of words — *"not great"* and *"great"* contribute the same conditional log-probability for *great*
- C. NB cannot handle Unicode
- D. NB lacks softmax

> [!success]- Answer
> **B.** Negation, sarcasm, and compositionality require context; bag-of-words+independence loses this signal.
