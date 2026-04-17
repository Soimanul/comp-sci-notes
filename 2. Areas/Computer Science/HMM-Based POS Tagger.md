**Tags:** #concept #nlp #pos #sequence-labelling
**Related:** [[POS Tagging]], [[Viterbi Algorithm]], [[Markov Assumption]]

## Definition

An HMM-based POS tagger models the joint probability of a word sequence $\mathbf{w}$ and tag sequence $\mathbf{t}$ as a product of emission and transition probabilities, then finds the most likely tag sequence via the Viterbi algorithm.

> [!info] Key Intuition
> The HMM tagger makes two assumptions: (1) a tag depends only on the previous tag (Markov), and (2) a word depends only on its own tag (emission). Together they let you factor a complex joint probability into simple lookup tables.

## Core Mechanics

**Generative model**:
$$P(\mathbf{w}, \mathbf{t}) = \prod_{i=1}^{n} P(t_i \mid t_{i-1}) \cdot P(w_i \mid t_i)$$

- **Transition probability** $P(t_i \mid t_{i-1})$: how likely is tag $t_i$ to follow $t_{i-1}$? (estimated from treebank counts)
- **Emission probability** $P(w_i \mid t_i)$: how likely is word $w_i$ given it has tag $t_i$?

**Decoding**: $\hat{\mathbf{t}} = \arg\max_{\mathbf{t}} P(\mathbf{w}, \mathbf{t})$ — solved by Viterbi in $O(n \cdot |T|^2)$ time.

**Smoothing**: unseen (word, tag) pairs get Laplace or Witten-Bell smoothed emission probabilities; unknown words handled by suffix heuristics or morphological rules.

> [!example]- Worked Example
> "Time flies like an arrow."
> Transition: $P(\text{NN} \mid \text{START}) > P(\text{VBZ} \mid \text{START})$
> Emission: $P(\text{"time"} \mid \text{NN}) > P(\text{"time"} \mid \text{VBZ})$
> Viterbi selects NN for "time" at position 1.

> [!warning] Common Misconception
> The HMM tagger sees only the previous tag — it is blind to the next word or the word before the previous. This bigram Markov assumption misses long-range syntactic dependencies that neural models capture naturally.
