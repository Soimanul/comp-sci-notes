**Tags:** #concept #nlp #embeddings
**Related:** [[Word Embeddings]], [[One-Hot Encoding]], [[Word2Vec]]

## Definition
An embedding matrix $E \in \mathbb{R}^{V \times d}$ stores one dense vector per vocabulary word, where $V$ is vocabulary size and $d \ll V$ is the embedding dimension. Each row is the learnable representation of one word.

Given a one-hot vector $x$ for a word, the embedding is obtained by
$$e = E^\top x$$
which simply selects the corresponding row of $E$.

> [!info] Key Intuition
> The embedding matrix is a learnable lookup table. The "matrix multiplication" with a one-hot vector is just row indexing — no real arithmetic happens; in code it is implemented as `E[word_id]`.

## Why It Replaces One-Hot
- **Compact**: $d$ is small (e.g., 100–768) vs. $V$ that can be hundreds of thousands.
- **Trainable**: rows are updated by backpropagation alongside the rest of the model.
- **Semantic**: words appearing in similar contexts end up with similar rows, so the matrix encodes meaning instead of just identity.

> [!example]- Worked Example
> Vocabulary {I, love, NLP}, $d = 2$. Initial $E$:
> $$E = \begin{pmatrix} 0.1 & 0.2 \\ 0.7 & -0.3 \\ 0.4 & 0.5 \end{pmatrix}$$
> One-hot for "love" is $x = (0, 1, 0)$, so $e = E^\top x = (0.7, -0.3)$ — the second row.

> [!warning] Common Misconception
> The embedding matrix is *not* fixed external knowledge bolted onto the network. It is part of the model's parameters and is learned end-to-end with the task loss (or pretrained on a separate language-modelling task and then fine-tuned).

## Significance
Embedding matrices are the bridge between discrete language and continuous neural computation. Every modern NLP architecture, from word2vec to transformers, starts with one.
