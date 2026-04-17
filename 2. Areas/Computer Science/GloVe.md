**Tags:** #concept #nlp #embeddings
**Related:** [[Word Embeddings]], [[Word2Vec]], [[Distributional Hypothesis]]

## Definition

GloVe (Global Vectors for Word Representation) learns word embeddings by factorising a log-transformed global word-word co-occurrence matrix. It combines the statistical efficiency of count-based methods with the predictive power of neural approaches.

> [!info] Key Intuition
> Word2Vec learns from local windows one at a time; GloVe looks at the whole corpus at once and asks: can two vectors' dot product predict how often their words co-occur globally?

## Core Mechanics

**Objective** — minimise weighted least squares over all co-occurring pairs:
$$J = \sum_{i,j=1}^{V} f(X_{ij})\left(\mathbf{w}_i^\top \tilde{\mathbf{w}}_j + b_i + \tilde{b}_j - \log X_{ij}\right)^2$$

where:
- $X_{ij}$ = co-occurrence count of words $i$ and $j$
- $f(X_{ij})$ = weighting function (caps influence of very frequent pairs)
- $\mathbf{w}_i$, $\tilde{\mathbf{w}}_j$ = word and context vectors
- $b_i$, $\tilde{b}_j$ = bias terms

Final embeddings = $\mathbf{w}_i + \tilde{\mathbf{w}}_j$ (sum of word and context vectors).

> [!example]- Worked Example
> Ratio test: $P(\text{ice} \mid \text{solid}) / P(\text{steam} \mid \text{solid}) \gg 1$. GloVe encodes this ratio difference as a vector offset, explaining why analogy arithmetic works: the ratio is captured geometrically.

> [!warning] Common Misconception
> GloVe and Word2Vec embeddings are not interchangeable drop-ins. GloVe trains on global co-occurrences and is typically better at capturing semantic relatedness; Word2Vec's local context window can capture syntactic patterns more sharply.
