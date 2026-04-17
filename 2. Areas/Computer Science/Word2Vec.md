**Tags:** #concept #nlp #embeddings
**Related:** [[Word Embeddings]], [[CBOW vs Skip-gram]], [[Distributional Hypothesis]]

## Definition

Word2Vec is a family of shallow neural network models that learn dense word representations by training on a self-supervised prediction task over local context windows. The two architectures are CBOW (predict centre word from context) and Skip-gram (predict context words from centre word).

> [!info] Key Intuition
> Word2Vec doesn't learn "what words mean" — it learns "what contexts words share." The meaning emerges as a byproduct of being good at prediction.

## Core Mechanics

**Training objective (Skip-gram)**:
$$\max \sum_{t} \sum_{-c \leq j \leq c, j \neq 0} \log P(w_{t+j} \mid w_t)$$

where $c$ is the context window size. The probability is modelled via softmax over a dot product between input and output embeddings.

**Negative sampling** approximates full softmax: for each positive (word, context) pair, sample $k$ random negative context words and train a binary classifier to distinguish them.

**Training produces two matrices**:
- $\mathbf{W}_{in}$: input embeddings (used as word representations)
- $\mathbf{W}_{out}$: output embeddings (usually discarded)

> [!example]- Worked Example
> Skip-gram, window = 2, sentence: *"the cat sat on the mat"*
> Centre word: *"sat"* → positive pairs: (sat, cat), (sat, the), (sat, on), (sat, the)
> For each positive pair, sample 5 negatives (random vocabulary words) and update weights via binary cross-entropy.

## Significance

Word2Vec demonstrated that word analogy arithmetic emerges from distributional training: $\vec{\text{king}} - \vec{\text{man}} + \vec{\text{woman}} \approx \vec{\text{queen}}$. This sparked the modern embedding era.
