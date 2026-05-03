**Tags:** #concept #nlp #sentiment
**Related:** [[Sentiment Lexicons]], [[Compositional Challenges in Lexicon Scoring]], [[Sentiment Analysis]]

## Definition

Once a sentiment lexicon assigns each word a real-valued score $\text{score}(w) \in \mathbb{R}$, classification becomes a deterministic aggregation. For a document $d = (w_1, \dots, w_n)$, the simplest length-normalised score is

$$S_{\text{norm}}(d) = \frac{1}{n} \sum_{i=1}^{n} \text{score}(w_i).$$

Classification is by thresholding at zero:

$$\hat{y} = \begin{cases} \text{positive} & \text{if } S(d) > 0 \\ \text{negative} & \text{if } S(d) < 0 \end{cases}$$

> [!info] Key Intuition
> No training is required — sentiment is "looked up" word-by-word and averaged. This makes lexicon scoring fully transparent and trivially explainable, but it also assumes additivity, independence, and context invariance that natural language rarely respects.

## Emotion-Vector Variant

If the lexicon encodes discrete emotion categories rather than scalar polarity, the document score is a **vector**:

$$S_k(d) = \sum_{i=1}^{n} \mathbf{1}[w_i \in \text{Emotion}_k]$$

for each emotion category $k$. The predicted emotion corresponds to the largest component.

> [!example]- Worked Example
> Sentence: *"I love this phone but the battery is terrible."*
> Lexicon: love $= +3$, terrible $= -3$. All other words: $0$.
> $S_{\text{norm}} = (3 - 3)/9 \approx 0$ → neutral.
> The aggregation cancels two strong opposing opinions about different aspects — the [[Aspect-Based Sentiment Analysis]] problem in miniature.

## Significance

Lexicon scoring is the baseline against which every other sentiment method is measured. Its assumptions — additivity, independence, context invariance — are explicit, which makes the failure modes (negation, sarcasm, domain shift) easy to diagnose. See [[Compositional Challenges in Lexicon Scoring]] for the structural failures this method cannot patch.
