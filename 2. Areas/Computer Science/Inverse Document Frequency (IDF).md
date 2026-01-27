**Tags:** #concept #nlp #information-retrieval #term-weighting  
**Related:** [[Term Weighting]] · [[Term Frequency (TF)]] · [[TF–IDF]] · [[Term–Document Matrix]]

## Definition
**Inverse Document Frequency (IDF)** downweights terms that appear in many documents and upweights terms that are rare across the corpus. IDF captures corpus-level informativeness.

## Intuition
- If a term appears in most documents, it carries little discriminative power for distinguishing documents.
- Rare terms are typically more informative about a document’s topic or content.

## Canonical form
Let:
- $N$ = total number of documents
- $df(t)$ = number of documents containing term $t$ (document frequency)

Then:
$$
idf(t)=\log\left(\frac{N}{df(t)}\right)
$$

## Smoothed variants (common in practice)
To avoid division by zero and reduce extremes:
$$
idf(t)=\log\left(\frac{N+1}{df(t)+1}\right)+1
$$

## Role in TF–IDF
IDF is combined with TF to produce a weight that is high when:
- the term is frequent in a document (TF high)
- but rare across the corpus (IDF high)

See [[TF–IDF]].

## Limitations (IDF alone)
- IDF does not model semantics; it only measures global rarity.
- A rare term can still be irrelevant to a specific query or document’s meaning without contextual matching.
