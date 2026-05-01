**Tags:** #concept #neural-networks #optimization
**Related:** [[Stochastic Gradient Descent (SGD)]], [[Momentum Gradient Descent]], [[Backpropagation]]

## Definition
Optimizers are algorithms that update neural-network parameters using the gradients computed by backpropagation. They differ in how they accumulate past gradient information and how they adapt the per-parameter step size.

> [!info] Key Intuition
> Plain SGD treats every parameter the same and trusts each gradient blindly. Modern optimizers add memory (momentum) and adaptivity (per-parameter learning rates) so noisy or sparse gradients don't destabilize training.

## Comparison

| Optimizer | Update idea | Strengths | When to use |
|---|---|---|---|
| **SGD** | $\theta \leftarrow \theta - \varepsilon \nabla L$ on a mini-batch | Simple, stable, well-understood | Large datasets, baselines |
| **SGD + Momentum** | Adds a velocity term $v \leftarrow \mu v + \nabla L$, then $\theta \leftarrow \theta - \varepsilon v$ | Faster convergence, smoother trajectory | Deep networks, vision |
| **Adam** | Adaptive per-parameter learning rate plus momentum | Very robust, sensible defaults | Default choice in NLP |
| **RMSProp** | Adaptive learning rate via moving average of squared gradients | Handles noisy gradients | RNN training |
| **Adagrad** | Per-parameter learning rate that shrinks as $\sum g^2$ grows | Helps sparse features | Word embeddings, NLP with sparse inputs |

## Learning Rate
The learning rate $\varepsilon$ is the most sensitive hyperparameter:
- Too small → slow training, may stall.
- Too large → oscillation around minima or even diverging loss.

> [!warning] Common Misconception
> Adam being "the default" doesn't mean it's always best. Vision benchmarks often beat Adam with well-tuned SGD + momentum. The choice depends on architecture, batch size, and gradient regime.

## Significance
The optimizer is one of the three pillars of training (alongside loss and architecture). A poor optimizer choice silently caps the achievable accuracy, even with a perfect model.
