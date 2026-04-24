**Tags:** #concept #ml
**Related:** [[Decision Trees]], [[Entropy for Decision Trees]]

## Definition

**Gini impurity** measures the probability that a randomly chosen sample from a node would be incorrectly classified if labelled randomly according to the node's class distribution.

$$G(t) = \sum_{k=1}^{K} p_k(t) \left(1 - p_k(t)\right) = 1 - \sum_{k=1}^{K} p_k(t)^2$$

Where $p_k(t)$ = proportion of class $k$ samples at node $t$.

> [!info] Key Intuition
> A pure node (all samples from one class) has Gini = 0. A maximally impure node (equal class distribution) has Gini = $1 - \frac{1}{K}$. The best split is the one that maximises the weighted Gini reduction (parent Gini minus the weighted average of children's Gini).

## Gini Reduction (Split Quality)

$$\Delta G = G(\text{parent}) - \frac{n_L}{n} G(\text{left}) - \frac{n_R}{n} G(\text{right})$$

The algorithm evaluates this for every feature and threshold, choosing the split with maximum $\Delta G$.

> [!example]- Binary Classification Example
> Node has 10 samples: 7 class A, 3 class B.
> $G = 1 - (0.7^2 + 0.3^2) = 1 - (0.49 + 0.09) = 0.42$
> 
> After split: left child has 6 A, 0 B → $G_L = 0$; right child has 1 A, 3 B → $G_R = 1 - (0.25 + 0.5625) = 0.375$
> $\Delta G = 0.42 - \frac{6}{10}(0) - \frac{4}{10}(0.375) = 0.42 - 0.15 = 0.27$

## Gini vs. Entropy

| Property | Gini | Entropy |
|---|---|---|
| Range | [0, 1 − 1/K] | [0, log₂ K] |
| Computation | Cheaper (no log) | Slightly more expensive |
| Behaviour | Slight bias toward larger partitions | More balanced |
| Default in sklearn | Yes | No (use criterion='entropy') |

## Significance

Gini is the default splitting criterion in scikit-learn's CART implementation and in most GBDT libraries. In practice the choice between Gini and Entropy rarely makes a significant difference in final model accuracy.
