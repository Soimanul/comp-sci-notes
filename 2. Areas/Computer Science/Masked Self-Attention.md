**Tags:** #concept #nlp #neural-networks
**Related:** [[Self-Attention]], [[Cross-Attention]], [[Transformer Architecture]]

## Definition
Masked (causal) self-attention is self-attention restricted so that each position can only attend to itself and earlier positions in the same sequence. Future positions are masked out by setting their attention scores to $-\infty$ before the softmax, which gives them zero weight.

$$\mathrm{score}_{ij} = \frac{q_i \cdot k_j}{\sqrt{d_k}} + M_{ij}, \quad M_{ij} = \begin{cases} 0 & j \leq i \\ -\infty & j > i \end{cases}$$

> [!info] Key Intuition
> The mask enforces "no peeking ahead". During training the entire target sequence is fed at once for parallelism, but each output position must behave as if it had only seen its predecessors — exactly the situation at inference time.

## Why Masking Is Needed
- **Autoregressive consistency**: at inference the decoder generates one token at a time; it cannot use future tokens because they don't exist yet.
- **Training/inference parity**: without masking, the model would learn to cheat by attending to the very tokens it is supposed to predict, breaking generation at test time.

> [!example]- Worked Example
> Decoder input "[BOS] hello world". Position 1 ("hello") can only attend to "[BOS]" and itself; position 2 ("world") attends to "[BOS]", "hello", and itself. The mask blocks attention from "[BOS]" to "hello" or "world", and from "hello" to "world".

> [!warning] Common Misconception
> Masking is applied *before* the softmax, not after. Replacing softmax weights with zeros after the fact would not normalize correctly and would change the relative weights of the remaining (visible) tokens.

## Significance
Masked self-attention is what turns a Transformer block into a left-to-right language model. It is the only architectural difference between a BERT-style encoder block and a GPT-style decoder block.
