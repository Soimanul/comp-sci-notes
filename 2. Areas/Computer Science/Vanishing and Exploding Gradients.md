**Tags:** #concept #neural-networks #training
**Related:** [[Backpropagation Through Time]], [[Recurrent Neural Networks]], [[Long-Range Dependencies in RNNs]]

## Definition
In deep or recurrent networks, gradients computed via backpropagation are products of many Jacobian matrices. When repeated multiplications shrink the gradient toward zero we have **vanishing gradients**; when they blow it up we have **exploding gradients**. Both prevent effective learning.

> [!info] Key Intuition
> Gradient flow through depth or time is a chain of multiplications. Like compound interest, multiplying many numbers smaller than 1 vanishes; multiplying many numbers larger than 1 explodes — and either way, the parameters far from the loss can't be trained.

## Mathematical Origin
For an RNN unrolled over $T$ steps, the gradient with respect to an early hidden state factors as:
$$\frac{\partial L}{\partial h_k} = \frac{\partial L}{\partial h_T} \prod_{t=k+1}^{T} \frac{\partial h_t}{\partial h_{t-1}}$$
Each factor's magnitude is governed by the singular values of the recurrent weight matrix $W$:
- Largest singular value $< 1$ → product shrinks → **vanishing**.
- Largest singular value $> 1$ → product grows → **exploding**.

## Symptoms
- **Vanishing**: early-time-step parameters barely update; the model effectively learns only from recent tokens, capping context length.
- **Exploding**: loss spikes to NaN; weights become huge.

## Mitigations

| Problem | Common Fixes |
|---|---|
| Vanishing | Gating (LSTM, GRU), residual/skip connections, ReLU activations, careful initialization (Xavier, He) |
| Exploding | Gradient clipping, weight regularization, smaller learning rate |

> [!warning] Common Misconception
> Vanishing gradients are not a bug of backpropagation — they are a property of the *function* being differentiated. Architectures like LSTM solve the issue by changing the function so the gradient path stays close to the identity.

## Significance
The vanishing-gradient problem is the single most important reason simple RNNs cannot capture long-range dependencies. Every major recurrent architecture since (LSTM, GRU, attention-based models) is partly an answer to it.
