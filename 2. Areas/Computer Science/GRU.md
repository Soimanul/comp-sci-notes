**Tags:** #concept #neural-networks #nlp
**Related:** [[LSTM]], [[Gating Mechanism]], [[Recurrent Neural Networks]], [[GRU for Recommendations]]

## Definition
The Gated Recurrent Unit (GRU) is a simplified gated RNN that merges LSTM's forget and input gates into a single update gate and drops the separate cell state. The hidden state itself carries the memory.

$$z_t = \sigma(W_z x_t + U_z h_{t-1})$$
$$r_t = \sigma(W_r x_t + U_r h_{t-1})$$
$$\tilde{h}_t = \tanh(W x_t + U (r_t \odot h_{t-1}))$$
$$h_t = (1 - z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t$$

> [!info] Key Intuition
> One gate ($z_t$) decides "how much to update toward the new candidate"; the complement ($1-z_t$) keeps the old state. GRU collapses LSTM's three-gate dance into a single interpolation between past and proposed.

## Components
| Component | Meaning |
|---|---|
| $z_t$ | Update gate — interpolation weight between $h_{t-1}$ and $\tilde{h}_t$ |
| $r_t$ | Reset gate — how much past state participates in the candidate |
| $\tilde{h}_t$ | Candidate hidden state |
| $h_t$ | Final hidden state for this step |

## GRU vs LSTM

| Aspect | LSTM | GRU |
|---|---|---|
| Gates | 3 (forget, input, output) | 2 (update, reset) |
| Memory | Separate cell state $c_t$ | Hidden state only |
| Parameters | More | ~25% fewer |
| Speed | Slower | Faster |
| Long-range power | Slightly stronger in some tasks | Comparable on most |

> [!warning] Common Misconception
> GRU is not strictly "weaker" than LSTM. Empirically the two are very close on most NLP benchmarks; GRU is often preferred for compute reasons. The right choice depends on the dataset, not on a universal ranking.

## Significance
GRUs showed that LSTM's full machinery is not always necessary, popularizing the idea of leaner gated cells. Together with LSTMs, they were the workhorse sequence model before transformers arrived.
