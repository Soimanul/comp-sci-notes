**Tags:** #concept #nlp #ner #sequence-labelling
**Related:** [[Named Entity Recognition]], [[BIO Tagging Scheme]], [[Neural POS Tagger]]

## Definition

A Conditional Random Field (CRF) is a discriminative probabilistic model that predicts the entire label sequence jointly, conditioning on the full input. In NLP, a linear-chain CRF is added as the final layer of NER and POS taggers to enforce global tag consistency.

> [!info] Key Intuition
> A softmax layer scores each position independently; a CRF layer scores the entire sequence and learns that certain tag transitions are globally impossible — like `I-PER` following `B-ORG`.

## Core Mechanics

**CRF objective** — maximise conditional log-likelihood:
$$P(\mathbf{y} \mid \mathbf{x}) = \frac{\exp\!\left(\sum_i \mathbf{w}^\top \mathbf{f}(y_{i-1}, y_i, \mathbf{x}, i)\right)}{Z(\mathbf{x})}$$

where $Z(\mathbf{x})$ is the partition function computed via the forward algorithm.

In a neural CRF (BiLSTM-CRF): the BiLSTM produces per-token emission scores; the CRF layer adds a learnable $|T| \times |T|$ transition score matrix.

**Decoding**: Viterbi algorithm finds the globally optimal label sequence in $O(n \cdot |T|^2)$.

> [!example]- Worked Example
> A softmax tagger predicts `O B-PER O I-ORG O` — the `I-ORG` after `O` is illegal. A CRF layer with a learned transition matrix assigns $-\infty$ to this transition, so Viterbi never outputs it.

> [!warning] Common Misconception
> CRFs model label-to-label transitions, not label-to-label causation. The transition matrix captures co-occurrence statistics from training data — it cannot reason about entities it hasn't seen labelled.
