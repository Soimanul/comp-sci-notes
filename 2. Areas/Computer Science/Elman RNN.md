**Tags:** #concept #neural-networks #nlp
**Related:** [[Recurrent Neural Networks]], [[Hidden State (RNN)]], [[Backpropagation Through Time]]

## Definition
The Elman RNN is the simplest recurrent architecture. At each time step $t$ it combines the current input $x_t$ with the previous hidden state $h_{t-1}$ to produce a new hidden state and an output:
$$a_t = b_h + W h_{t-1} + U x_t$$
$$h_t = \tanh(a_t)$$
$$o_t = b_o + V h_t$$
$$\hat{y}_t = \mathrm{softmax}(o_t)$$

The hidden state $h_0$ is typically initialized to zero. The matrices $U, W, V$ and biases $b_h, b_o$ are shared across all time steps.

> [!info] Key Intuition
> The unfolded diagram shows many cells, but there is exactly one cell with one set of weights. Each step of the sequence applies the *same* function — recurrence is parameter sharing across time.

## Components
- $E$: embedding matrix that maps tokens to input vectors $x_t$
- $U$: input-to-hidden weights
- $W$: hidden-to-hidden (recurrent) weights
- $V$: hidden-to-output weights
- $b_h, b_o$: biases

## Forward Pass Summary
$$\text{token} \xrightarrow{E} x_t \xrightarrow{U,W,b_h,\tanh} h_t \xrightarrow{V,b_o,\text{softmax}} \hat{y}_t$$

> [!warning] Common Misconception
> The unfolded view is a *visual* expansion for backpropagation through time — it does not mean each step has its own weights. Confusing this leads people to wildly overestimate the parameter count of an RNN.

## Significance
Elman RNNs were the first successful neural sequence model and introduced the core idea — a recurrent hidden state — that survives in LSTMs, GRUs, and even in the recurrent state of transformer KV caches.
