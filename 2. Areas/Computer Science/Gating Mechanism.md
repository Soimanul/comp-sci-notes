**Tags:** #concept #neural-networks #nlp
**Related:** [[LSTM]], [[GRU]], [[Vanishing and Exploding Gradients]]

## Definition
A gate is a learnable, sigmoid-valued vector $g \in (0, 1)^d$ used as an elementwise multiplier to control how much of an information stream passes through. Concretely, given a candidate vector $u$, the gate produces $g \odot u$ — values close to 0 block, values close to 1 let through.

> [!info] Key Intuition
> A gate is a learned soft switch. Plain RNNs always overwrite the hidden state at every step; a gate lets the network decide what to keep, what to update, and what to throw away — turning an unstable recurrence into a controlled dynamical system.

## Mechanics
- Each gate is computed from the input and previous hidden state: $g = \sigma(W x_t + U h_{t-1})$.
- The sigmoid squashes outputs to $(0, 1)$, giving smooth, differentiable switches.
- Gates are combined elementwise with cell or hidden states, so each dimension is regulated independently.

> [!example]- Worked Example
> A forget gate $f_t = \sigma(W_f x_t + U_f h_{t-1})$ controls how much of the previous cell state to keep:
> $$c_t = f_t \odot c_{t-1} + i_t \odot \tilde{c}_t$$
> If $f_t \approx 1$, the cell preserves long-term memory; if $f_t \approx 0$, it forgets the past entirely.

> [!warning] Common Misconception
> Gates do not "select tokens" — they are continuous, differentiable, per-dimension multipliers. Hard, discrete selection would block backpropagation.

## Significance
Gating is the design pattern that makes long-context recurrent learning possible. The same idea — sigmoid-controlled multiplication — recurs in highway networks, GRU's update gate, attention masks, and even mixture-of-experts routing.
