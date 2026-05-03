**Tags:** #concept #nlp #ner #sequence-labelling
**Related:** [[Named Entity Recognition]], [[HMM-Based POS Tagger]], [[Viterbi Algorithm]], [[BIO Tagging Scheme]]

## Definition

The classical probabilistic solution for NER treats entity tags (in IOB/BIO form) as **hidden states** in a Hidden Markov Model and words as **observable emissions**. Mathematically the model is identical in form to the [[HMM-Based POS Tagger]] — only the interpretation of the hidden states changes.

> [!info] Key Intuition
> Hidden states are no longer grammatical categories — they are **referential** entity tags (B-PER, I-PER, B-LOC, O, …). The HMM machinery is unchanged; what shifts is *what the states mean*.

## Generative Model

Two assumptions:

- **Emission independence**: each word depends only on its tag.
$$P(w_1^n \mid t_1^n) = \prod_{i=1}^{n} P(w_i \mid t_i)$$
- **First-order Markov**: each tag depends only on the previous tag.
$$P(t_1^n) = \prod_{i=1}^{n} P(t_i \mid t_{i-1})$$

Joint model:

$$\hat{t}_1^{\,n} = \arg\max_{t_1^n} \prod_{i=1}^{n} P(w_i \mid t_i) \, P(t_i \mid t_{i-1}).$$

Words are observable; tags are hidden. Decoding ("which hidden sequence produced these observations?") is exactly what [[Viterbi Algorithm]] solves.

## Two Different Problems

| Problem | What is given | What is computed | Solver |
|---|---|---|---|
| **Decoding** | parameters + observations | most likely hidden sequence | Viterbi |
| **Learning** | only observations | initial / transition / emission probabilities | Baum–Welch (EM) |

In supervised NER the learning problem is trivial — counts from a labelled corpus, with smoothing. The hard case (Baum–Welch) arises only with unlabelled data.

## Viterbi Recursion (NER form)

Let $V_t(j) = $ best path probability ending in state $j$ at position $t$:

$$V_t(j) = \max_{i} \, V_{t-1}(i) \, a_{ij} \, b_j(w_t),$$

with backpointers

$$\psi_t(j) = \arg\max_{i} \, V_{t-1}(i) \, a_{ij}$$

allowing trajectory reconstruction. $a_{ij}$ are tag transitions, $b_j(w_t)$ are emissions.

> [!example]- Worked Example (Eisner 2002 ice-cream analogue)
> Climatologist sees only the number of ice creams eaten each day (1–3) and wants to recover the daily weather (Hot or Cold). Ice creams are emissions; weather is hidden state. The Viterbi trellis applied to this toy problem demonstrates exactly the same algorithm used for NER — only the alphabets change. For NER: ice creams ↔ words; weather ↔ entity tags.

## Why HMMs Are Not the Final Word

- Local dependencies only — cannot see beyond the previous tag.
- Strong generative assumptions — emission depends on the tag alone, ignoring rich context features (capitalisation, suffix, gazetteer hits).
- Errors compound through the trellis when emissions are weakly informative.

These limits are exactly what [[CRF for Sequence Labelling]] addresses by switching to a discriminative log-linear model with arbitrary features.

## Significance

The HMM is the conceptual baseline for every later NER system. Understanding it makes the design choices of CRFs and transformer-based taggers legible: each later model is a deliberate relaxation of an HMM assumption — richer features, longer context, deeper composition, or all three.
