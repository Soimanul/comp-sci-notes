**Tags:** #topic #hub #nlp
**Related:** [[Natural Language Processing]], [[Text Classification]], [[Maximum Entropy Classifier]]

## Overview
Logistic Regression is a central model for text classification in NLP. While it can be seen as a simple neural unit, in this course it is framed as a **Maximum Entropy Classifier**: a probabilistic model that makes the weakest possible assumptions while remaining consistent with observed data.

## Knowledge Map
### 1. Conceptual Foundations
- [[Maximum Entropy Classifier]]
- [[Entropy (in Information Theory)]]

### 2. The Model
- [[Sigmoid Function]]
- [[Log-Odds]]
- [[Feature Functions]]

### 3. Training

- [[Cross-Entropy Minimization]]
- [[Gradient Descent]]

## Mechanics

1. **Compute Score**: $z = \mathbf{w}^T \mathbf{x} + b$ (see [[Log-Odds]]).

2. **Apply Sigmoid**: $\hat{y} = \sigma(z) = \frac{1}{1+e^{-z}}$ (see [[Sigmoid Function]]).

3. **Decision Rule**: Typically, we assign Class 1 if $\hat{y} > 0.5$ (or $z > 0$).

## Significance
Unlike the Perceptron, Logistic Regression provides a measure of certainty (probability) and can be optimized using gradient-based methods even when data is not perfectly separable. In NLP, it is often referred to as a Maximum Entropy classifier, emphasizing its role in making unbiased probabilistic predictions.

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** Logistic regression is a *discriminative* classifier because it directly models:
- A. $P(x|y)$
- B. $P(y|x)$
- C. $P(x, y)$
- D. $P(x)$

> [!success]- Answer
> **B.** Discriminative models go straight for the conditional; this is the structural contrast with generative Naïve Bayes.

**2.** The *log-odds* (logit) of a probability $p$ is defined as:
- A. $\log\frac{p}{1-p}$
- B. $\log p$
- C. $\frac{1}{1+e^{-p}}$
- D. $p \cdot \log p$

> [!success]- Answer
> **A.** Logit maps $(0,1)$ to $(-\infty, +\infty)$, allowing a *linear* function to predict it without bounding constraints.

**3.** The sigmoid is the inverse of:
- A. Tanh
- B. The logit (log-odds)
- C. Softmax
- D. Cross-entropy

> [!success]- Answer
> **B.** $\sigma(z) = 1/(1+e^{-z})$ inverts $\log(p/(1-p))$ — sigmoid takes you back to probability space.

**4.** Maximum entropy framing says the classifier should:
- A. Minimize entropy
- B. Maximize entropy of $P(y|x)$ subject to expected feature constraints from data — the most uncommitted distribution consistent with what we know
- C. Ignore features
- D. Match the prior exactly

> [!success]- Answer
> **B.** MaxEnt picks the *least* assumption-laden distribution that still satisfies observed feature expectations.

**5.** Why is cross-entropy the natural loss for logistic regression?
- A. It is the negative log-likelihood under a Bernoulli/Categorical model — minimizing it is MLE
- B. It is faster than MSE
- C. It is convex by accident
- D. It uses fewer parameters

> [!success]- Answer
> **A.** Cross-entropy = NLL for sigmoid/softmax outputs; minimizing it estimates the parameters that make the data most likely.

**6.** A feature function in MaxEnt typically:
- A. Returns a real number indicating the activation of some attribute given an input–class pair
- B. Always returns 0
- C. Returns a probability
- D. Is a one-hot vector

> [!success]- Answer
> **A.** Feature functions $f_i(x,y)$ encode hand-designed or learned indicators tied to specific (input, class) configurations.

**7.** Logistic regression's decision boundary is:
- A. Linear in the input feature space
- B. Always quadratic
- C. Non-existent
- D. Depends on the kernel

> [!success]- Answer
> **A.** Even though the output is non-linear, the boundary $z=0$ is a hyperplane $\mathbf{w}^\top\mathbf{x} + b = 0$.

**8.** Compared to the perceptron, logistic regression:
- A. Outputs probabilities and is trainable on non-separable data
- B. Cannot use gradient descent
- C. Has no bias term
- D. Cannot handle multiclass

> [!success]- Answer
> **A.** Sigmoid + log-likelihood gives smooth gradients; the perceptron rule has no notion of probability and gets stuck on non-separable data.

**9.** L2 regularization on logistic regression's weights pushes them toward 0. The probabilistic interpretation is:
- A. A Gaussian prior $N(0, \sigma^2)$ on the weights
- B. A Laplace prior
- C. A uniform prior
- D. A Dirichlet prior

> [!success]- Answer
> **A.** Adding $\lambda \|\mathbf{w}\|^2$ to the loss is equivalent to MAP under a zero-mean Gaussian prior on weights.

**10.** L1 regularization differs from L2 in that:
- A. It produces *sparse* weight vectors — many weights driven exactly to 0 — implying feature selection
- B. It is non-differentiable everywhere
- C. It always converges faster
- D. It uses softmax

> [!success]- Answer
> **A.** L1's geometry has corners; the optimum lands on axis-aligned vertices, zeroing out features.

**11.** A logistic regression with weight $w_j = 2$ on feature $x_j$ means:
- A. A unit increase in $x_j$ increases the *odds* of class 1 by a factor of $e^2 \approx 7.39$
- B. Probability increases by 2
- C. The log-loss increases by 2
- D. The accuracy changes by 2%

> [!success]- Answer
> **A.** Weights are interpretable in log-odds space; exponentiating gives the multiplicative effect on odds.

**12.** Multinomial logistic regression (softmax regression) generalizes binary LR by:
- A. Using softmax over class scores: $P(y=c|x) = \frac{e^{z_c}}{\sum_{c'} e^{z_{c'}}}$
- B. Using sigmoid per class independently
- C. Using a different feature representation
- D. Using L1 regularization

> [!success]- Answer
> **A.** Softmax produces a normalized categorical distribution over classes.

**13.** Why is the cross-entropy loss for LR convex?
- A. Because softmax/sigmoid composed with NLL yields a convex function in the parameters; gradient descent finds the global optimum
- B. Because of L2 regularization
- C. By accident
- D. Because features are non-negative

> [!success]- Answer
> **A.** This is the key practical advantage over neural networks — no local minima issue.

**14.** A practitioner compares Naïve Bayes and logistic regression on the same text-classification dataset. Which is *generally* true?
- A. NB outperforms LR with very little data; LR overtakes as data grows
- B. LR is always worse
- C. They are mathematically identical
- D. NB never overfits

> [!success]- Answer
> **A.** Ng & Jordan (2001) — generative models converge to their (higher) asymptotic error faster, discriminative models reach a lower asymptotic error eventually.

**15.** Logistic regression assumes features are conditionally independent given the class:
- A. True
- B. False — LR makes no such assumption; it learns weights jointly
- C. Only with L2
- D. Only for binary tasks

> [!success]- Answer
> **B.** This is exactly where LR is *less* "naïve" than NB: correlated features get correctly down-weighted.

**16.** When is logistic regression's MLE solution *undefined* / divergent?
- A. When data is perfectly linearly separable — weights grow unboundedly to push probabilities to 0/1
- B. When data has no labels
- C. When features are normalized
- D. When using softmax

> [!success]- Answer
> **A.** Without regularization, perfect separability allows $\|\mathbf{w}\| \to \infty$ to keep increasing likelihood.

**17.** The entropy of a Bernoulli with $p=0.5$ is:
- A. 0 bits
- B. 1 bit (maximum)
- C. 0.5 bits
- D. 2 bits

> [!success]- Answer
> **B.** Maximum uncertainty for a binary outcome is 1 bit; that is the MaxEnt baseline before constraints.

**18.** Cross-entropy between predicted distribution $\hat{p}$ and one-hot true label $y$ reduces to:
- A. $-\log \hat{p}_y$ — the negative log-probability of the true class
- B. $\hat{p}_y - 1$
- C. $-\sum \hat{p}$
- D. The L2 norm

> [!success]- Answer
> **A.** A clean simplification because $y$ is one-hot — only the true-class term survives.

**19.** A logistic regressor's prediction $\hat{y} = 0.51$ means:
- A. The model is highly confident
- B. The model assigns slightly above 50% to class 1 — calibration of this confidence is a separate concern
- C. The classifier is broken
- D. The boundary is at infinity

> [!success]- Answer
> **B.** Probabilities near 0.5 indicate uncertainty; raw outputs are not always calibrated.

**20.** An advantage of LR over the perceptron in text classification is:
- A. Smooth, differentiable loss enables principled optimization, regularization, and probability estimates
- B. LR uses fewer features
- C. LR is faster
- D. LR cannot overfit

> [!success]- Answer
> **A.** Differentiability + convexity + probabilistic interpretation make LR the workhorse baseline.

**21.** Stochastic Gradient Descent on LR converges to:
- A. A local minimum specific to the seed
- B. The global minimum of the convex loss (with appropriate learning rate schedule)
- C. The Bayes-optimal classifier
- D. A saddle point

> [!success]- Answer
> **B.** Convexity guarantees a unique global minimum (up to weight ties on degenerate features).

**22.** Why is logistic regression sometimes called the "single-neuron neural network"?
- A. Because $z = w^Tx+b$ followed by sigmoid is exactly one logistic neuron with no hidden layers
- B. Because it has one output
- C. Because it cannot use ReLU
- D. By marketing convention

> [!success]- Answer
> **A.** This is the structural connection: deep nets stack many such units; LR is the degenerate one-unit case.
