**Tags:** #concept #neural-networks #nlp
**Related:** [[Elman RNN]], [[Recurrent Neural Networks]], [[Long-Range Dependencies in RNNs]]

## Definition
In an RNN, the hidden state $h_t$ is a vector that summarizes the information seen in the input sequence up to time $t$. Formally:
$$h_t = f(x_1, x_2, \dots, x_t)$$
The hidden state is *not* a parameter — it is a learned representation that is recomputed for every new sequence.

> [!info] Key Intuition
> The hidden state is the network's working memory. At each step the model rewrites this memory using the previous state and the new token, and the final state is its compressed account of the whole sequence.

## How It Evolves
Reading "I like natural language processing":
- $h_1 \approx$ representation of "I"
- $h_2 \approx$ representation of "I like"
- $h_3 \approx$ representation of "I like natural"
- $h_4 \approx$ representation of "I like natural language"
- $h_5 \approx$ representation of the full sentence

Each update applies the same recurrent function: $h_t = \tanh(W h_{t-1} + U x_t + b)$.

> [!example]- Worked Example
> For sentiment classification, only $h_T$ (the final state) is fed to the classifier — it is treated as the encoder's verdict on the whole input. For language modelling, *every* intermediate $h_t$ is used to predict the next token.

> [!warning] Common Misconception
> Hidden states are not stored between sentences. Once inference on a sequence ends, $h_T$ is typically discarded; new sequences re-initialize $h_0$ to zeros (unless explicitly carrying state, e.g. truncated BPTT).

## Significance
The hidden state is the conceptual centerpiece of any recurrent model. Architectural innovations in LSTMs, GRUs, and gated recurrences all amount to *better mechanisms for updating this hidden state*.
