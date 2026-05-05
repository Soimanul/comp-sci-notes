**Tags:** #hub #nlp #sentiment
**Related:** [[Natural Language Processing]], [[Naïve Bayes]], [[Logistic Regression]]

## Overview

Sentiment Analysis (Opinion Mining) is the computational study of opinions, sentiments, emotions, and appraisals expressed in text toward an entity or one of its features. It ranges from coarse-grained document-level polarity classification to fine-grained aspect-level analysis, and extends to **sentiment trajectories** that treat tone as a temporal signal across discourse.

> [!abstract]- TL;DR
> An opinion is formally a quintuple $(e, a, s, h, t)$. Most practical systems collapse it to a single polarity label $s$ and predict it with three competing perspectives — n-gram language models, Naïve Bayes, or logistic regression — or aggregate lexicon scores. Beyond static classification, sentiment can be tracked sentence-by-sentence to expose discourse and rhetorical structure.

## Knowledge Map

### 1. What Sentiment Is
- [[Opinion Mining]]
- [[Subjectivity vs Objectivity in Text]]
- [[Sentiment Triple]]
- [[Opinion Quintuple]]

### 2. Lexicon-Based Approaches
- [[Sentiment Lexicons]]
- [[Lexicon Scoring]]
- [[Compositional Challenges in Lexicon Scoring]]
- [[VADER]]

### 3. Three Perspectives on Sentiment Classification
- [[Three Perspectives on Sentiment Classification]]
- [[Naïve Bayes]]
- [[Logistic Regression]]

### 4. Sentiment Beyond Documents
- [[Aspect-Based Sentiment Analysis]]
- [[Sentiment as Temporal Signal]]

> [!question]- Common Exam Questions
> - Write down the opinion quintuple and explain each component.
> - What is the difference between an opinion, a sentiment, and an emotion?
> - State the lexicon-based scoring formula and explain how negation breaks it.
> - Compare the n-gram, Naïve Bayes, and logistic regression formulations of sentiment classification — what does each fundamentally ask?
> - How does treating sentiment as a temporal signal change what the analysis reveals?
> - Why is the Loughran–McDonald lexicon needed for financial text?

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** The opinion quintuple $(e, a, s, h, t)$ is intentionally rich because it forces the analyst to commit to:
- A. The vocabulary
- B. *Who* held *what* sentiment about *which aspect of which entity at what time*
- C. The classifier architecture
- D. The training corpus

> [!success]- Answer
> **B.** Coarse polarity loses entity, aspect, holder, and time. The quintuple is a checklist of what coarse models throw away.

**2.** A review states: *"The screen is gorgeous but the battery life is awful."* Document-level classification fails this review specifically because:
- A. The review is too short
- B. The document mixes opposing sentiments toward different aspects; a single label loses information
- C. Lexicon scoring cannot detect adjectives
- D. Naïve Bayes always predicts neutral

> [!success]- Answer
> **B.** This is the canonical motivation for *aspect-based* sentiment analysis.

**3.** A lexicon-based scorer assigns +1 to *good* and -1 to *bad*. It fails on *"not good"* because:
- A. *not* is OOV
- B. Lexicon scoring is non-compositional — it sums word polarities ignoring negation scope and modifiers
- C. *good* has no synonym
- D. Lexicons are case-sensitive

> [!success]- Answer
> **B.** The compositional challenge: meaning of phrases is not a sum of word meanings.

**4.** VADER's design specifically improves over plain lexicon sums by:
- A. Encoding intensifiers, negations, capitalization, punctuation, and emojis as score modifiers
- B. Replacing the lexicon with a neural network
- C. Using softmax
- D. Stripping all punctuation

> [!success]- Answer
> **A.** VADER is hand-engineered for social-media affect signals (ALL CAPS, !!!, "very", emoji).

**5.** Why is the Loughran–McDonald lexicon used for financial text instead of a general affect lexicon?
- A. It is shorter
- B. General lexicons mis-score domain terms — *"liability"*, *"risk"*, *"exposure"* are negative in everyday English but neutral/technical in finance
- C. It contains emoji
- D. It is multilingual

> [!success]- Answer
> **B.** Domain-specific affect lexicons exist precisely because polarity is context-bound.

**6.** Subjectivity classification asks:
- A. Is this text positive or negative?
- B. Is this text expressing an opinion at all, regardless of polarity?
- C. Who is the holder?
- D. What is the entity?

> [!success]- Answer
> **B.** Subjectivity is upstream of polarity: filter to opinionated text *before* asking which way it leans.

**7.** Which scenario is *uniquely* well served by aspect-based sentiment analysis?
- A. A binary spam filter
- B. A product team triaging which features to prioritize from thousands of mixed reviews
- C. A topic model
- D. A spell checker

> [!success]- Answer
> **B.** ABSA decomposes feedback by feature; document-level polarity is too coarse for this kind of decision.

**8.** The fundamental difference between *opinion*, *sentiment*, and *emotion* is best framed as:
- A. They are synonymous
- B. Opinions are stance toward an object; sentiments are valenced affective states; emotions are specific affect categories (anger, joy)
- C. Emotions are computed first
- D. Sentiments are always neutral

> [!success]- Answer
> **B.** Useful hierarchy: opinion (about something) → sentiment (positive/negative tone) → emotion (specific affective label).

**9.** Treating sentiment as a *temporal signal* across a document reveals:
- A. The vocabulary
- B. Rhetorical structure — turning points, escalation, narrative arcs that aggregate scoring hides
- C. Document length
- D. Subjectivity only

> [!success]- Answer
> **B.** A novel may average to neutral while traversing extremes; the trajectory exposes structure the average loses.

**10.** A logistic-regression sentiment classifier with bag-of-words features fails on *"This phone is not bad at all."* The cleanest single explanation is:
- A. *bad* dominates as a strongly-negative feature; the model has no way to encode the long-range negation scope
- B. *bad* is OOV
- C. The bias is wrong
- D. The model is overfitting

> [!success]- Answer
> **A.** Negation scope and idiomatic litotes ("not bad") are exactly what BoW + linear models cannot capture.

**11.** Naïve Bayes can in principle outperform logistic regression on small sentiment datasets because:
- A. NB has stronger inductive bias and converges faster, even though its asymptotic error is higher
- B. NB is exact
- C. NB ignores priors
- D. NB has no hyperparameters

> [!success]- Answer
> **A.** Classic generative-vs-discriminative trade-off — NB wins early, LR wins eventually.

**12.** *Sarcasm* is a notorious failure case for sentiment classifiers because:
- A. Sarcastic text often uses positive vocabulary to express negative sentiment, inverting surface signals
- B. It uses Unicode
- C. It is rare
- D. Lexicons are too small

> [!success]- Answer
> **A.** *"Just what I needed today, another bug"* — every word is positive but the meaning isn't.

**13.** Which feature engineering choice would *most* help on tweets?
- A. Removing all punctuation and emoji
- B. Preserving emoji, hashtags, repeated punctuation, and elongations as separate features
- C. Lowercasing aggressively
- D. Stripping mentions

> [!success]- Answer
> **B.** Social-media affect lives in the very surface signals that "clean" preprocessing throws away.

**14.** *Aspect extraction* in ABSA typically uses:
- A. POS-tag-based heuristics (frequent nouns), supervised tagging, or neural sequence models to find aspect terms
- B. Random selection
- C. TF–IDF only
- D. Logistic regression on full documents

> [!success]- Answer
> **A.** Aspects are typically nouns; extraction can be unsupervised (frequency + POS) or supervised (BIO tagging).

**15.** A model trained on *movie* reviews drops sharply when applied to *restaurant* reviews. The phenomenon is:
- A. Cross-domain shift — vocabulary, aspects, and norms differ; lexical features don't transfer cleanly
- B. Class imbalance
- C. Underfitting
- D. Tokenization

> [!success]- Answer
> **A.** *"Cheesy"* is positive for pizza, negative for a film; transfer requires domain adaptation or larger pretrained representations.

**16.** Why are *neutral* labels often harder than positive/negative?
- A. They are richer
- B. Neutral texts mix factual and weakly-affective content; the boundary with mild positive/negative is fuzzy and annotator-dependent
- C. They are shorter
- D. They contain no nouns

> [!success]- Answer
> **B.** Annotator agreement on neutrals is notoriously low; this propagates to model performance.

**17.** A sentiment classifier outputs P(positive) = 0.51 for a document. This says:
- A. The model is confident
- B. Slightly above chance toward positive — calibration matters before triggering downstream actions
- C. Document is neutral
- D. Sentiment is undefined

> [!success]- Answer
> **B.** Probability near 0.5 = the model is hedging; production systems should use thresholds and calibration.

**18.** Why is sarcasm detection often framed as a *separate* upstream task?
- A. It requires features (context, contrast, world knowledge) that sentiment models alone struggle with; pipelining gives a chance to flip the polarity
- B. Sarcasm is part of POS tagging
- C. It is solved
- D. Sarcasm has no features

> [!success]- Answer
> **A.** Detect sarcasm first → then invert/adjust the polarity prediction; works better than expecting a single model to learn both.

**19.** A *temporal* sentiment plot of a customer support transcript shows a sudden negative spike in the third paragraph. The actionable interpretation is:
- A. The transcript is negative overall
- B. There is a localized escalation point worth investigating — aggregate scoring would have hidden it
- C. The transcript is neutral
- D. Tokenization failed

> [!success]- Answer
> **B.** The whole point of temporal sentiment is to surface localized signal aggregate metrics smooth away.

**20.** Which architecture *decisively* outperforms classical sentiment classifiers on benchmarks like SST-2?
- A. Pretrained Transformers (BERT/RoBERTa) fine-tuned on labels
- B. Multinomial Naïve Bayes
- C. Logistic regression with TF–IDF
- D. Lexicon scoring

> [!success]- Answer
> **A.** Contextual embeddings handle negation, sarcasm, and compositionality far better than BoW models.

**21.** A stakeholder asks for a sentiment score that reflects *intensity*, not just polarity. The cleanest engineering response is:
- A. Use sigmoid output as a continuous score, or use VADER's compound score, or train a regression head on rated reviews
- B. Use only argmax
- C. Bag-of-words can't be intense
- D. Train Naïve Bayes only

> [!success]- Answer
> **A.** Intensity is naturally captured by continuous outputs; argmax discards exactly that.

**22.** The *deepest* reason BoW + classical classifiers ceiling out on sentiment is:
- A. They are slow
- B. They have no context-sensitive representation of words; meaning lives in composition (negation, intensifiers, ABSA), and BoW destroys composition
- C. Lexicons are wrong
- D. Sigmoid is wrong

> [!success]- Answer
> **B.** Sentiment is structurally compositional; BoW's loss of word order and dependency is the structural cap.
