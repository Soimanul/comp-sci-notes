**Tags:** #concept #nlp #sentiment
**Related:** [[Sentiment Analysis]], [[Naïve Bayes]], [[Logistic Regression]], [[Statistical Language Models]]

## Definition

Three classical models all aim to predict the sentiment component $s$ of the [[Opinion Quintuple]] from the linguistic realisation of a text, but they conceptualise the inference problem in fundamentally different ways:

- **N-gram language model** — *which class makes this sentence more probable?*
- **Naïve Bayes** — *which class accumulates more lexical evidence?*
- **Logistic regression** — *on which side of the optimal decision boundary does this sentence lie?*

> [!info] Key Intuition
> Sentiment can be framed as **differential fluency** (n-gram), **aggregated lexical evidence** (NB), or **geometric separation** (LR). Same task, three different stories about what classification *is*.

## The N-gram Perspective

Estimate a separate language model per sentiment class and pick the class under which the sentence is most likely:

$$P(x \mid s) = \prod_{i=1}^{T} P(w_i \mid w_{i-1}, \dots, w_{i-n+1}, s)$$

$$\hat{s} = \arg\max_{s} P(x \mid s) P(s)$$

Sentiment is inferred by asking which **generative hypothesis** better explains the surface realisation. Captures local sequential regularities; does not represent target entity or aspect.

## The Naïve Bayes Perspective

Word counts $c_j$ contribute additively to log-posterior:

$$\log P(s \mid x) = \log P(s) + \sum_{j=1}^{p} c_j \log P(w_j \mid s)$$

with smoothing

$$P(w_j \mid s) = \frac{c_{j,s} + \alpha}{N_s + \alpha V}.$$

Sentiment is **aggregated lexical evidence**: each word independently shifts the score toward one class. Order is discarded; conditional independence is assumed once $s$ is fixed.

## The Logistic Regression Perspective

Discriminative — no generative story:

$$P(s = 1 \mid x) = \frac{1}{1 + e^{-(\beta_0 + \boldsymbol{\beta}^{\top} \mathbf{x})}}$$

Parameters are obtained by minimising cross-entropy. The model learns a **separating surface** in feature space that best discriminates sentiment categories.

## Side-by-Side

| Aspect | N-gram | Naïve Bayes | Logistic Regression |
|---|---|---|---|
| Generative or discriminative | Generative | Generative | Discriminative |
| Word order | Yes (within window) | No | No |
| Conditional independence | No | Yes | Not assumed in same sense |
| What is learned | $P(w \mid \text{context}, s)$ | $P(w \mid s)$ and $P(s)$ | Decision boundary |
| Question asked | Which $s$ generates $x$? | Which $s$ explains the words? | Which side of the boundary? |

> [!warning] Common Misconception
> Naïve Bayes and logistic regression with the same features often perform similarly on small data, but they are not interchangeable. NB uses MLE on conditional probabilities; LR optimises a discriminative loss directly. With more data, LR usually wins; with very little, NB's stronger prior helps.

## Significance

These three perspectives recur throughout NLP: text classification, language modelling, and structured prediction all reuse the same generative-vs-discriminative split. Recognising which question a model asks clarifies what kind of error it will make and what kind of feature engineering will help.
