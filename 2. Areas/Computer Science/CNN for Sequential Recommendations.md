**Tags:** #concept #reco #dl
**Related:** [[Sequential vs Session-Based Recommendation]], [[Dilated Convolutions for Recommendations]], [[GRU for Recommendations]]

## Definition

**CNN for Sequential Recommendations (Caser)** applies convolutional filters over a user's recent interaction embeddings to capture both point-level (individual item) and union-level (item set) sequential patterns.

> [!info] Key Intuition
> A 1D horizontal filter slides over the time axis, capturing "what subsequences of items tend to lead to this next item." Vertical filters aggregate across items for set-based patterns. Unlike RNNs, CNNs process all positions in parallel.

## Caser Architecture (Convolutional Sequence Embedding)

**Input:** Embed the $L$ most recent items into a matrix $E \in \mathbb{R}^{L \times d}$ (L items × d embedding dimensions).

**Horizontal filters (temporal patterns):**
- $n_h$ filters of height $h$ and width $d$: capture subsequences of length $h$
- Each filter → 1D output → max-pooling → scalar
- Applied for $h = 1, 2, \ldots, L$

**Vertical filters (set patterns):**
- $n_v$ filters of height $L$ and width $1$: collapse across all $L$ items
- Output: $d$-dimensional vector per filter

**Prediction:**
$$\hat{r}_{u,t} = \phi^h \oplus \phi^v \oplus p_u \to \text{FC} \to \text{score}$$

## Advantages Over RNNs

| Property | RNN (GRU/LSTM) | CNN (Caser) |
|---|---|---|
| Parallelism | Sequential — slow to train | Fully parallel across time |
| Order sensitivity | Implicitly via hidden state | Explicitly via filter position |
| Union-level patterns | Hard to capture | Natural (vertical filters) |
| Long-range dependency | Better (full hidden state) | Limited to filter width |

> [!warning] Fixed Window
> Caser only considers the last $L$ interactions, discarding older history. The optimal $L$ is a hyperparameter. Dilated convolutions extend this range without proportionally increasing parameters.

## Significance

Caser demonstrated that CNNs can outperform RNN-based sequential models while being faster to train due to parallelism. Its explicit treatment of union-level patterns is a key contribution.
