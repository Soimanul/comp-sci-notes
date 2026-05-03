**Tags:** #concept #nlp #pos #sequence-labelling
**Related:** [[POS Tagging]], [[Naïve Bayes]], [[HMM-Based POS Tagger]]

## Definition

Part-of-Speech tagging is **structured prediction**: given a sequence of words $w_1, \dots, w_n$, the goal is to predict the most probable sequence of tags

$$\hat{t}_1, \dots, \hat{t}_n = \arg\max_{t_1, \dots, t_n} P(t_1, \dots, t_n \mid w_1, \dots, w_n).$$

The output is not a single label but a **joint configuration** of labels whose components are interdependent.

> [!info] Key Intuition
> Conceptually, POS tagging is Naïve Bayes for sequences. The same machinery — conditional probabilities, count-based estimation, smoothing, likelihood maximisation — is reused; the only new ingredient is that **predictions at different positions constrain each other**.

## Connection with Naïve Bayes

In Naïve Bayes spam classification:

$$P(\text{class} \mid \text{document}).$$

In POS tagging:

$$P(\text{tag sequence} \mid \text{word sequence}).$$

Same shape, same estimation tools — the conceptual shift is from a **single label** to a **structured output**. There is no fundamental departure from probabilistic classification, just a generalisation.

## Why Structure Matters

Tagging each word independently throws away the statistical signal that comes from neighbouring tags. *"can"* between a pronoun and a verb behaves very differently from *"can"* between a determiner and a noun. Structured prediction lets the model resolve word-level ambiguity using **sequence context**.

> [!example]- Worked Example
> *"They can fish"*
> Independent tagging cannot decide between PRON–MOD–VERB and PRON–NOUN–NOUN.
> Sequence model compares full sequences and picks the one with higher transition × emission product. Context resolves ambiguity statistically.

## Significance

This framing — "tagging = structured Naïve Bayes" — makes the leap to HMMs natural and shows that classical NLP is a continuous progression: bag-of-words classifiers → sequence classifiers → neural sequence models. The structural idea (predictions are not independent) is what every later sequence model, including transformers, also exploits.
