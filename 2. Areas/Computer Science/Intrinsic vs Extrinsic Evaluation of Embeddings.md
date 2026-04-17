**Tags:** #concept #nlp #embeddings
**Related:** [[Word Embeddings]], [[Word2Vec]], [[GloVe]]

## Definition

Intrinsic evaluation measures embedding quality on dedicated word-vector benchmarks (similarity, analogy) in isolation. Extrinsic evaluation measures the impact of embeddings on a downstream task (NER, sentiment classification, machine translation).

> [!info] Key Intuition
> A model that aces the analogy test can still hurt a downstream task — intrinsic benchmarks measure geometric structure, not task utility. Always prefer extrinsic evaluation for production decisions.

## Core Mechanics

**Intrinsic benchmarks**:
| Task | Dataset | Metric |
|---|---|---|
| Word similarity | SimLex-999, WordSim-353 | Spearman $\rho$ vs human ratings |
| Analogy | Google Analogy (Mikolov) | % correct via $\vec{a}-\vec{b}+\vec{c}$ |
| Clustering | — | Purity of semantic clusters |

**Extrinsic evaluation**: swap embedding layer in a downstream model (NER tagger, sentiment classifier), retrain or fine-tune, compare task metrics (F1, accuracy).

**Trade-offs**:
- Intrinsic: fast, cheap, reproducible — but weakly predictive of task performance
- Extrinsic: directly relevant — but expensive and confounded by model architecture

> [!example]- Worked Example
> GloVe scores higher than Word2Vec on SimLex-999 (semantic similarity). Yet on NER tagging, Word2Vec embeddings yield higher F1 because the local context window captures more syntactic information useful for tagging.

> [!warning] Common Misconception
> High analogy-test accuracy does not imply the embeddings capture "true" meaning. The analogy test rewards linear structure in a specific geometric configuration — a useful proxy, but not meaning itself.
