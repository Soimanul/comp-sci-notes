**Tags:** #concept #nlp #embeddings
**Related:** [[Word2Vec]], [[Word Embeddings]], [[Static Embedding Limits]]

## Definition

The space learned by Word2Vec (and similar predictive embeddings) is linear, but its structure is **shaped by training**. Words appearing in similar contexts are pulled together; words in distinct contexts are pushed apart. Many semantic and syntactic relations correspond to approximate **linear translations** in this space.

> [!info] Key Intuition
> Direction encodes relation. The vector difference $v_{\text{king}} - v_{\text{man}}$ approximates a "royalty" direction; adding $v_{\text{woman}}$ moves to the corresponding female royal — landing close to $v_{\text{queen}}$.

## The Analogy Test

Empirically:

$$v_{\text{king}} - v_{\text{man}} + v_{\text{woman}} \approx v_{\text{queen}}.$$

Many relational pairs follow the same pattern:

| Relation | Example |
|---|---|
| Capital–country | $v_{\text{Paris}} - v_{\text{France}} + v_{\text{Italy}} \approx v_{\text{Rome}}$ |
| Verb tense | $v_{\text{walked}} - v_{\text{walk}} + v_{\text{run}} \approx v_{\text{ran}}$ |
| Comparative | $v_{\text{bigger}} - v_{\text{big}} + v_{\text{small}} \approx v_{\text{smaller}}$ |
| Plural | $v_{\text{dogs}} - v_{\text{dog}} + v_{\text{cat}} \approx v_{\text{cats}}$ |

This linear-substructure phenomenon suggests **relational information is stored in directions**, not just in absolute positions.

## Contrast with LSA

In LSA the axes correspond to directions of maximal **variance** — they have a global statistical interpretation. In learned embeddings the axes have **no individual semantic meaning**: meaning is distributed across all dimensions, and only certain *directions* (not basis vectors) align with relations.

> [!warning] Common Misconception
> Analogy arithmetic is not perfect. The nearest neighbour to $v_{\text{king}} - v_{\text{man}} + v_{\text{woman}}$ in vocabulary is often *king* itself — most evaluations exclude the input words from the candidate set. Reported accuracy figures depend heavily on this preprocessing detail.

## Significance

Linear analogy success is the empirical fingerprint of distributional learning succeeding: it shows the space has internalised structured semantic regularities, not merely surface co-occurrence. It also bounds what embeddings cannot do — see [[Static Embedding Limits]].
