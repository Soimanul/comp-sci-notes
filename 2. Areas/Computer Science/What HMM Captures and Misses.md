**Tags:** #concept #nlp #pos #sequence-labelling
**Related:** [[HMM-Based POS Tagger]], [[POS Tagging]], [[Recurrent Neural Networks]], [[Transformer Architecture]]

## Definition

The Hidden Markov Model is a **bigram** sequence model: each tag depends only on the immediately previous tag, and each word depends only on its own tag. This independence structure makes Viterbi tractable but caps what the model can express.

> [!info] Key Intuition
> The HMM is a bridge: it shows that grammatical structure can be modelled probabilistically and that ambiguity can be resolved statistically — but it cannot see beyond the previous tag, and it cannot represent hierarchy or meaning.

## What the HMM Does Capture

- **Frequent tag transitions** — e.g. DET → NOUN is much more likely than DET → VERB.
- **Typical word–category associations** — emission $P(w \mid t)$ encodes which words usually take which tag.
- **Local grammatical regularities** — short-range patterns like article + adjective + noun.
- **Statistical disambiguation** — chooses the most probable sequence rather than enumerating all valid ones.

## What the HMM Does Not Capture

- **Long-distance syntactic dependencies** — subject-verb agreement across an embedded clause is invisible to a bigram model.
- **Hierarchical structure** — phrases nested inside phrases (constituency or dependency trees).
- **Semantic interpretation** — meaning is not represented; tags are purely grammatical.
- **Word-internal cues at scale** — morphological structure must be hand-engineered (suffix tables for unknown words).
- **Bidirectional context** — only the previous tag conditions the current one; the future is invisible during emission.

## Why This Matters

These limits define the design space for what came next:

| HMM limit | Architectural answer |
|---|---|
| Bigram tag context | Higher-order HMMs, then RNNs |
| One-directional view | Bi-LSTM tagger |
| Tag-only conditioning on word | CRFs add rich features over the entire sentence |
| No hierarchy | Constituency / dependency parsers |
| No semantics | Embedding-based and transformer models |

> [!warning] Common Misconception
> "HMMs are obsolete." They remain useful when training data is scarce, interpretability matters, or compute is constrained. Their limits are structural, not practical — for many low-resource tagging tasks they are still a strong baseline.

## Significance

HMM POS tagging is the canonical example of how **independence assumptions** trade expressive power for tractable inference. Every later sequence model can be read as a deliberate relaxation of one of HMM's assumptions: extending the context, replacing tag-only dependence with rich features, or replacing fixed Markov structure with learned attention.
