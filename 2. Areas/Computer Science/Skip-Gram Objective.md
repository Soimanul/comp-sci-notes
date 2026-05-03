**Tags:** #concept #nlp #embeddings
**Related:** [[Word2Vec]], [[CBOW vs Skip-gram]], [[Negative Sampling]], [[Word Embeddings]]

## Definition

In the Skip-Gram model, each word $w$ has a learnable vector $v_w \in \mathbb{R}^d$ (and a context vector $u_w$). For a centre word $w$ and context word $c$, the conditional probability is a softmax over dot products:

$$P(c \mid w) = \frac{\exp(u_c^{\top} v_w)}{\sum_{w' \in V} \exp(u_{w'}^{\top} v_w)}.$$

> [!info] Key Intuition
> Words whose vectors have **large dot products** are predicted as likely neighbours. Training adjusts vectors so that true (centre, context) pairs are scored high — meaning becomes geometry through repeated prediction.

## The Training Objective

Given a corpus $w_1, \dots, w_T$ and a fixed context window of size $c$, maximise

$$\prod_{t=1}^{T} \prod_{c \in \mathcal{C}(w_t)} P(c \mid w_t),$$

or equivalently the log-likelihood

$$\sum_{t=1}^{T} \sum_{c \in \mathcal{C}(w_t)} \log P(c \mid w_t).$$

Optimisation is by **stochastic gradient descent** on the centre and context embedding matrices $W, U \in \mathbb{R}^{V \times d}$ (typically randomly initialised).

## The Computational Problem

The softmax denominator sums over the entire vocabulary. Realistic numbers: $V \approx 100{,}000$, window size 5, corpus size $10^8$ tokens → roughly $10^9$ training pairs, each requiring a sum over $10^5$ words. The full softmax is intractable.

Two standard approximations: **hierarchical softmax** (binary tree over vocabulary) and **negative sampling** (see [[Negative Sampling]]). The latter dominates in practice.

> [!example]- Worked Example
> Sentence *"the cat sat on the mat"*, window $= 2$, centre $= $ "sat".
> Positive pairs: (sat, the), (sat, cat), (sat, on), (sat, the).
> Each contributes a $\log P(c \mid \text{sat})$ term, encouraging $u_c^{\top} v_{\text{sat}}$ to be high relative to dot products with random vocabulary words.

## Significance

Skip-Gram established the predictive paradigm: rather than decomposing a global co-occurrence matrix (LSA), structure emerges from **local prediction objectives** optimised by gradient descent. The geometry of the resulting space is shaped by what predicts what — not by what variance dimension dominates.
