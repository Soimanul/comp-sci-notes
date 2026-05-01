**Tags:** #concept #nlp #embeddings
**Related:** [[Word Embeddings]], [[Embedding Matrix]], [[Feedforward Neural Network]]

## Definition
A simple way to represent a variable-length sentence as a single fixed-size vector by averaging the embeddings of its words. For a sentence of $T$ words with embeddings $e_1, \dots, e_T$:
$$s = \frac{1}{T} \sum_{t=1}^{T} e_t$$

> [!info] Key Intuition
> Mean pooling collapses a sequence of word vectors into a single point in embedding space. Two sentences with similar word distributions land near each other regardless of length.

## Pipeline
A neural classifier built on this idea has the shape:
$$\text{words} \rightarrow \text{embeddings} \rightarrow \text{average} \rightarrow \text{feedforward classifier} \rightarrow \text{label}$$

> [!example]- Worked Example
> Sentence: "I love NLP" with embeddings $(0.1, 0.2)$, $(0.7, -0.3)$, $(0.4, 0.5)$.
> Average: $s = ((0.1+0.7+0.4)/3, (0.2-0.3+0.5)/3) = (0.4, 0.133)$.
> This 2-dim vector is then fed to a feedforward network for classification.

> [!warning] Common Misconception
> Averaging discards word order entirely — "dog bites man" and "man bites dog" produce the same vector. It works as a strong baseline for topic-style classification but fails for tasks where syntax matters (sentiment with negation, NLI, QA), motivating sequence models like RNNs and transformers.

## Significance
Mean-pooled embeddings are the simplest neural sentence encoder. Their strong performance on many tasks set a baseline that more complex sequence models had to beat, and the same pooling trick is still used inside larger architectures (e.g., as a sentence representation after BERT).
