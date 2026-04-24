**Tags:** #concept #ml
**Related:** [[Decision Trees]], [[Gini Index]]

## Definition

**Entropy** (information entropy) measures the impurity of a node in a decision tree as the expected information content (surprise) of the class label distribution.

$$H(t) = -\sum_{k=1}^{K} p_k(t) \log_2 p_k(t)$$

The **information gain** of a split is:

$$IG = H(\text{parent}) - \frac{n_L}{n} H(\text{left}) - \frac{n_R}{n} H(\text{right})$$

> [!info] Key Intuition
> Entropy is zero when a node is pure (all one class — no uncertainty). Entropy is maximum (log₂ K bits) when all K classes are equally represented — maximum uncertainty. A good split maximises the reduction in entropy (information gain).

## Range

- Binary classification: Entropy ∈ [0, 1] bit
- K-class: Entropy ∈ [0, log₂ K] bits

> [!example]- Example
> Node: 7 positive, 3 negative.
> $H = -(0.7 \log_2 0.7 + 0.3 \log_2 0.3) = -(0.7 \times (-0.515) + 0.3 \times (-1.737))$
> $H \approx 0.361 + 0.521 = 0.882$ bits

## Information Gain Ratio

Plain information gain favours features with many values (e.g. ID features that create pure leaves trivially). The **gain ratio** corrects for this:

$$\text{GainRatio} = \frac{IG}{H(\text{split})}$$

where $H(\text{split}) = -\sum \frac{n_c}{n} \log_2 \frac{n_c}{n}$ is the entropy of the split itself. Used in C4.5.

## Significance

Entropy-based information gain was used in ID3 and C4.5 (the precursors to modern decision tree implementations). CART (scikit-learn default) uses Gini for speed, but both criteria produce very similar trees in practice.
