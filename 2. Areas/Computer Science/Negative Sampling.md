**Tags:** #concept #nlp #embeddings
**Related:** [[Skip-Gram Objective]], [[Word2Vec]], [[Word2Vec PMI Equivalence]]

## Definition

Negative sampling replaces the full softmax in [[Skip-Gram Objective]] with a much cheaper **binary classification** objective: distinguish each observed (centre, context) pair from $k$ randomly sampled "noise" pairs. The per-pair objective is

$$\log \sigma(u_c^{\top} v_w) + \sum_{i=1}^{k} \log \sigma(-u_{n_i}^{\top} v_w),$$

where $\sigma$ is the logistic sigmoid and $n_i$ are noise words sampled from a unigram-based distribution.

> [!info] Key Intuition
> Instead of normalising over the entire vocabulary, contrast the true context against a handful of random words. The model learns to push real pairs close and push random pairs apart — local geometry shaped by **contrast**, not by partition functions.

## Why It Works

Each training step turns into logistic regression on $k+1$ word pairs:

- 1 positive pair: $(w, c)$ that actually co-occurred.
- $k$ negative pairs: $(w, n_i)$ where $n_i$ is sampled from the noise distribution $P_n(w) \propto \text{count}(w)^{3/4}$ (the $3/4$ power downweights very frequent words without ignoring them).

Computational cost per pair drops from $O(V)$ to $O(k+1)$ — typically $k = 5$ to $20$.

## Practical Implications

- **$k$ small** (5–20) for large datasets.
- **$k$ large** (10–25) for small datasets where each pair must carry more signal.
- The $3/4$ unigram distribution outperforms both uniform and pure unigram noise empirically.

> [!warning] Common Misconception
> Negative sampling is not the same as noise-contrastive estimation (NCE). NCE provably approximates the softmax in the limit; negative sampling drops the normalisation term and only approximately corresponds to a softmax — but it works very well in practice for embedding learning.

## Significance

Negative sampling made Word2Vec scalable to billion-token corpora and is the proximate reason large-scale pretrained embeddings became practical. It is also the conceptual hinge that links Word2Vec to matrix factorisation (see [[Word2Vec PMI Equivalence]]).
