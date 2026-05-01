**Tags:** #concept #training #neural-networks
**Related:** [[Backpropagation]], [[Recurrent Neural Networks]], [[Vanishing and Exploding Gradients]]

## Definition
Backpropagation Through Time (BPTT) is the application of standard backpropagation to the unfolded computation graph of a recurrent network. The RNN cell, applied $T$ times across the sequence, is unrolled into a feedforward graph with $T$ shared-weight layers; gradients are then computed by the usual chain rule.

> [!info] Key Intuition
> BPTT is just backprop on the unrolled graph — the only twist is that the same parameter appears in many layers, so its total gradient is the *sum* of the per-step gradients.

## Mechanism
1. **Forward pass**: feed the entire sequence through the cell, storing $x_t$ and $h_t$ at each step.
2. **Loss aggregation**: compute per-step loss $L_t$ (usually negative log-likelihood of the next token) and total loss $L = \sum_t L_t$ (or its average).
3. **Backward pass**: traverse time in reverse, accumulating $\partial L / \partial \theta$ for each shared parameter $\theta \in \{U, W, V, b_h, b_o\}$ across all time steps.
4. **Update**: apply gradient descent (SGD, Adam, ...) to the shared parameters.

## Practical Variants
- **Truncated BPTT**: backpropagate gradients only through the last $k$ time steps. Saves memory and prevents extreme gradient magnitudes, at the cost of ignoring very long-range dependencies during training.

> [!warning] Common Misconception
> BPTT is not a different optimization algorithm — it is plain backpropagation applied to a graph with weight sharing. Saying "the RNN learns by BPTT" is equivalent to saying "the RNN learns by backprop on its unfolded graph".

## Significance
BPTT made it possible to train recurrent networks at all, but it also exposed their core training pathology: gradients have to traverse many time steps, and each step multiplies by the recurrent weight matrix. This product is the source of the vanishing/exploding gradient problem.
