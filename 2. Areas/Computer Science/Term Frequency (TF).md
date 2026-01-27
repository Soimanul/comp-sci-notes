**Tags:** #concept #nlp #information-retrieval #term-weighting  
**Related:** [[Term Weighting]] · [[Inverse Document Frequency (IDF)]] · [[TF–IDF]] · [[Bag-of-Words (BoW)]]

## Definition
**Term Frequency (TF)** measures how strongly a term is associated with a specific document based on how often it appears in that document. TF is the within-document component of term weighting.

## Intuition
- A term that appears more often in a document is more likely to reflect the document’s content.
- Raw counts can be misleading because very frequent terms can dominate similarity even when they are not informative.

## Common TF variants
### Raw count
$$
tf(t,d)=f(t,d)
$$
where $f(t,d)$ is the number of occurrences of term $t$ in document $d$.

### Log-scaled TF
$$
tf(t,d)=
\begin{cases}
1+\log f(t,d) & \text{if } f(t,d)>0 \\
0 & \text{otherwise}
\end{cases}
$$
Used to reduce the impact of very large counts.

### Length-normalized TF (conceptual)
TF may be normalized by document length to reduce bias toward longer documents (often handled separately via vector normalization).

## Role in TF–IDF
TF captures **document-specific salience**, while IDF downweights terms that are common across the corpus. The product defines TF–IDF:
- see [[TF–IDF]].

## Limitations (TF alone)
- Overweights common function words without an IDF-like correction.
- Confounds topical relevance with document length and repetition effects unless combined with normalization/IDF.
