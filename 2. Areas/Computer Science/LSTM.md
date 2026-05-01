**Tags:** #concept #neural-networks #nlp
**Related:** [[Gating Mechanism]], [[GRU]], [[Recurrent Neural Networks]], [[LSTM for Recommendations]]

## Definition
The Long Short-Term Memory (LSTM) cell augments the standard RNN with an explicit cell state $c_t$ and three gates — forget, input, and output — that regulate the flow of information through that state.

$$f_t = \sigma(W_f x_t + U_f h_{t-1})$$
$$i_t = \sigma(W_i x_t + U_i h_{t-1})$$
$$\tilde{c}_t = \tanh(W_c x_t + U_c h_{t-1})$$
$$c_t = f_t \odot c_{t-1} + i_t \odot \tilde{c}_t$$
$$o_t = \sigma(W_o x_t + U_o h_{t-1})$$
$$h_t = o_t \odot \tanh(c_t)$$

> [!info] Key Intuition
> The cell state $c_t$ is a highway: information flows through it across time with mostly elementwise operations, so gradients don't have to pass through repeated nonlinear matrix multiplications. The three gates decide what to erase, what to write, and what to expose.

## Roles of the Components
| Component | Meaning |
|---|---|
| $f_t$ | Forget gate — what to erase from old memory $c_{t-1}$ |
| $i_t$ | Input gate — what to write from the candidate $\tilde{c}_t$ |
| $\tilde{c}_t$ | Candidate cell — proposed new memory contents |
| $c_t$ | Cell state — the long-term memory |
| $o_t$ | Output gate — what part of the cell to expose as $h_t$ |
| $h_t$ | Hidden state — externally visible representation |

> [!example]- Worked Example
> Reading "The cat that I saw yesterday **was** black": when the cell encounters "cat", $i_t$ writes "subject = cat (sg.)"; through the rest of the modifier, $f_t$ keeps that information mostly intact; at "was", the network exposes it via $o_t$ to choose the singular verb.

> [!warning] Common Misconception
> The hidden state $h_t$ is *not* the memory — it is a *gated view* of the cell state $c_t$. The actual long-term store is $c_t$, which never gets squashed by tanh during the carry update.

## Significance
LSTMs were the first architecture to robustly capture long-range dependencies in language and speech, dominating sequence modelling from the late 1990s until transformers. The gating pattern they introduced is reused in nearly every recurrent or recurrent-style model since.
