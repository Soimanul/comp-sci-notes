**Tags:** #concept #neural-networks #nlp
**Related:** [[Recurrent Neural Networks]], [[Information Bottleneck (Encoder-Decoder)]], [[Attention Mechanism]]

## Definition
The encoder–decoder (sequence-to-sequence) architecture splits sequence-to-sequence problems into two networks:
- **Encoder** consumes the input sequence and produces an internal representation (a context vector or sequence of hidden states).
- **Decoder** is a conditional language model that generates the output sequence one token at a time, conditioned on the encoder's representation.

> [!info] Key Intuition
> The encoder learns *what* the input means with respect to the task; the decoder learns *how* to express that meaning in the target sequence. Neither is meaningful alone — they share a learned communication space.

## Anatomy
- Encoder: an RNN (or LSTM/GRU) that processes $x_1, \dots, x_T$ and produces a final hidden state (or full sequence of states) used by the decoder.
- Decoder: an autoregressive RNN that, at each step, takes the previously generated token and the encoder context and predicts the next token: $p(y_u \mid y_{<u}, x_{1:T})$.
- Trained jointly to maximize $P(y_1, \dots, y_U \mid x_1, \dots, x_T)$.

## Training
- Requires parallel data: pairs $(x^{(i)}, y^{(i)})$, e.g. (Spanish sentence, English translation).
- The encoder has **no direct loss** — it is only trained through the decoder's gradient. It is a parametric transformation shaped by the decoder's needs.
- The decoder has the actual cross-entropy loss against the target sequence; gradients flow back through it into the encoder.
- An epoch is a full forward + backward pass through both networks for every training pair.

## Use Cases
- Machine translation
- Text summarization
- Speech-to-text
- Question answering

> [!warning] Common Misconception
> The encoder is not a language model of the source language — it never produces a probability distribution over source tokens. Its only job is to package the input into a representation the decoder can use.

## Significance
Encoder–decoder is the first architecture that handled variable-length input and output sequences end-to-end. It established the pattern still used by transformer-based seq2seq models (T5, mBART, NMT systems), with attention later replacing the single-vector context.
