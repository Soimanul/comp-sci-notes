**Tags:** #topic #hub #nlp
**Related:** [[Natural Language Processing]], [[Deep Learning Architectures]]

## Overview
This hub bridges classical NLP pipelines (Bag-of-Words, TF–IDF, statistical classifiers) and the neural framework, where the model itself learns input representations jointly with the prediction task. It covers the building blocks of feedforward neural networks, how parameters are learned through gradient-based optimization, and how words — discrete symbols — are mapped to dense vectors that a neural model can consume.

> [!abstract]- TL;DR
> Feedforward neural networks compose parameterized linear layers with nonlinear activations to learn task-specific representations. For NLP they sit on top of an embedding lookup that maps words to dense vectors, and parameters are trained end-to-end by minimizing a loss with backpropagation.

## Knowledge Map

### 1. Building Blocks
- [[Single Neuron Computation]]
- [[Layer Vector Computation]]
- [[Feedforward Neural Network]]
- [[Activation Functions]]

### 2. Training
- [[Backpropagation]]
- [[Epoch]]
- [[Stochastic Gradient Descent (SGD)]]
- [[Neural Network Loss Functions]]
- [[Neural Network Optimizers]]

### 3. From Words to Vectors
- [[One-Hot Encoding]]
- [[Embedding Matrix]]
- [[Word Embeddings]]

### 4. Neural Text Classification
- [[Sentence Average Embedding]]

> [!question]- Common Exam Questions
> - Why are nonlinear activation functions essential in a multi-layer network?
> - How does the embedding matrix relate to the one-hot encoding of a word?
> - What changes when moving from Batch GD to SGD to Mini-Batch GD?
> - Given a sentence, describe a minimal neural pipeline that classifies it.

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** Stacking linear layers with no activation collapses to:
- A. A non-linear function
- B. A single equivalent linear transformation — the depth gains no expressive power
- C. A convolution
- D. A softmax

> [!success]- Answer
> **B.** Composition of linear maps is linear; non-linear activations are what give depth its modeling power.

**2.** ReLU avoids saturation for positive inputs because:
- A. Its derivative is 1 (not vanishing) on the positive side; only negatives have zero gradient
- B. It is bounded
- C. It is symmetric around 0
- D. It uses softmax

> [!success]- Answer
> **A.** This is why ReLU dramatically eased training of deep nets compared to sigmoid/tanh.

**3.** "Dead ReLU" refers to:
- A. A neuron whose weights drive its pre-activation negative for all inputs; gradient is 0 forever
- B. A removed neuron
- C. A neuron with infinite gradient
- D. A neuron that uses sigmoid

> [!success]- Answer
> **A.** Once dead, no signal flows; Leaky ReLU and proper initialization mitigate this.

**4.** The embedding matrix $E \in \mathbb{R}^{|V| \times d}$ relates to one-hot input $\mathbf{x}$ as:
- A. $E^\top \mathbf{x}$ — the multiplication selects the column corresponding to the index where $\mathbf{x}_i = 1$
- B. Matrix inverse
- C. Element-wise product
- D. Normalization

> [!success]- Answer
> **A.** "Embedding lookup" = pick a row by index; in autograd it is implemented as a sparse matrix multiply.

**5.** Cross-entropy loss for a softmax classifier with one-hot labels reduces to:
- A. $-\log \hat{p}_y$
- B. The L2 norm
- C. Mean squared error
- D. Hinge loss

> [!success]- Answer
> **A.** Pure NLL of the true class.

**6.** Adam differs from vanilla SGD by:
- A. Maintaining first- and second-moment estimates of gradients per parameter, giving adaptive learning rates
- B. Using larger batches
- C. Removing momentum
- D. Replacing softmax

> [!success]- Answer
> **A.** Combines momentum + RMSProp; default for many NLP setups.

**7.** Mini-batch SGD trades off batch GD and pure SGD by:
- A. Computing gradients on a subset (e.g., 32–256 examples) — better gradient estimates than pure SGD, far cheaper than batch GD
- B. Using one example always
- C. Using the full dataset always
- D. Avoiding randomization

> [!success]- Answer
> **A.** The standard practical compromise; also benefits from GPU vectorization.

**8.** A feedforward classifier over averaged word embeddings of a sentence:
- A. Computes the mean of token vectors and feeds it through dense layers — simple, position-agnostic, surprisingly strong on topical tasks
- B. Uses no embeddings
- C. Requires RNNs
- D. Computes self-attention

> [!success]- Answer
> **A.** "Deep Averaging Networks" (Iyyer 2015) — competitive baseline for many tasks.

**9.** Why does *averaging* embeddings fail on sentiment with negation?
- A. Mean pooling discards order; *"not good"* averages roughly to *"good"* + *"not"*, losing scope
- B. Averaging is non-differentiable
- C. Mean is too small
- D. It produces NaN

> [!success]- Answer
> **A.** Order matters for negation; mean pooling is the wrong inductive bias.

**10.** Backpropagation requires the loss to be:
- A. Differentiable (almost everywhere) with respect to the parameters
- B. Convex
- C. Bounded
- D. Symmetric

> [!success]- Answer
> **A.** Subgradient methods handle the "almost everywhere" cases (e.g., ReLU at 0).

**11.** Vanishing gradients in deep MLPs arise primarily because:
- A. Repeated multiplication of small derivatives (e.g., sigmoid in <1) shrinks gradients exponentially with depth
- B. Activations are too large
- C. The optimizer is wrong
- D. Embedding matrices are too small

> [!success]- Answer
> **A.** This is the chain-rule pathology that ReLU + careful initialization (He, Xavier) fix.

**12.** A classifier with 3 classes uses softmax + cross-entropy. Its gradient w.r.t. logit $z_i$ for the true class $y$ is:
- A. $\hat{p}_i - 1\{i=y\}$
- B. $\hat{p}_i + 1$
- C. $-\log \hat{p}_i$
- D. $\hat{p}_i \cdot 2$

> [!success]- Answer
> **A.** "Softmax minus one-hot" — clean closed-form gradient that makes implementations simple.

**13.** L2 regularization on weights is implemented as:
- A. Adding $\lambda \|\mathbf{w}\|^2$ to the loss; it acts as weight decay during gradient descent
- B. Setting weights to 0
- C. Using sigmoid
- D. Using dropout

> [!success]- Answer
> **A.** Standard regularizer; equivalent to a Gaussian prior on weights.

**14.** Dropout regularizes by:
- A. Randomly zeroing a fraction of unit activations during training, preventing co-adaptation
- B. Adding L2
- C. Pruning the network
- D. Using softmax

> [!success]- Answer
> **A.** Approximates ensembling many subnetworks; standard NLP recipe.

**15.** Why is initialization (Xavier, He) important?
- A. Bad initialization causes signals or gradients to vanish/explode through layers; principled scales preserve variance through depth
- B. It is a regularizer
- C. It speeds up softmax
- D. It removes bias

> [!success]- Answer
> **A.** Initialization sets the starting point of optimization; bad starts can be unrecoverable.

**16.** A single neuron computes:
- A. $a = \phi(\mathbf{w}^\top \mathbf{x} + b)$ — affine then non-linearity
- B. $a = \mathbf{w}^\top \mathbf{x} \cdot b$
- C. $a = \mathbf{w} + \mathbf{x} + b$
- D. $a = \phi(\mathbf{x})$

> [!success]- Answer
> **A.** The textbook formula.

**17.** Why does an *embedding layer* use far fewer parameters than a one-hot followed by a dense layer?
- A. The embedding maps $|V|$ → $d$ directly; a dense layer following one-hot would have $|V| \cdot d$ params with the same effective computation but no efficiency gain
- B. Embeddings have no parameters
- C. Embeddings are sparse
- D. Embeddings remove softmax

> [!success]- Answer
> **A.** They're the same parameter count in principle, but embedding lookups skip the wasteful one-hot multiplication entirely.

**18.** The softmax output of a network is best interpreted as:
- A. Posterior probabilities under the model's assumed distribution; calibrated only if training and test distributions match
- B. True probabilities
- C. Logits
- D. Distances

> [!success]- Answer
> **A.** Modern nets are often miscalibrated; temperature scaling or calibration methods help.

**19.** Why does using *the same* embedding matrix as input and output (weight tying) help language models?
- A. It reduces parameters and ties input and output semantics into one space, often improving perplexity
- B. It speeds up softmax
- C. It removes loss
- D. It breaks training

> [!success]- Answer
> **A.** Weight tying is a clean parameter-sharing trick used in many LM/Transformer setups.

**20.** A *deeper* network is not always better because:
- A. Optimization, generalization, and gradient flow get harder; depth needs residual connections, normalization, and data to scale
- B. Depth always overfits
- C. Depth is illegal
- D. Depth removes embeddings

> [!success]- Answer
> **A.** Plain MLP depth saturates without architectural support (residuals/LayerNorm).

**21.** A common reason loss explodes during training is:
- A. Learning rate too high — parameters overshoot, activations explode, gradients become NaN
- B. The optimizer is broken
- C. Data is correct
- D. Embeddings are too small

> [!success]- Answer
> **A.** Lower the LR or add gradient clipping; this is the textbook first fix.

**22.** The deepest reason neural NLP supplanted classical pipelines is:
- A. End-to-end joint learning of representations *and* decisions, sharing parameters and gradients across the whole task
- B. Neural networks are faster
- C. Classical models are illegal
- D. Neural models do not need data

> [!success]- Answer
> **A.** Hand-crafted features lose; learned features win — provided you have data and compute.
