**Tags:** #concept #nlp #generation
**Related:** [[Sequence Language Modelling]], [[Recurrent Neural Networks]], [[Elman RNN]]

## Definition
Text generation with an RNN is the autoregressive process of repeatedly sampling the next token from the model's predicted distribution and feeding it back as input. Starting from a prompt, the model produces text one token at a time until an end-of-sequence (EOS) token is emitted.

> [!info] Key Intuition
> Generation is the inference-time companion of language modelling. Training teaches "what is the next word likely to be?"; generation answers "let's pick one and ask again."

## Process
1. Encode the prompt into a hidden state $h_t$.
2. Compute $p(w_{t+1} \mid w_1, \dots, w_t)$ via softmax over the output layer.
3. Pick the next token. Common choices:
   - **Greedy**: argmax of the distribution.
   - **Sampling**: draw stochastically from the distribution.
   - **Top-k** / **top-p**: sample restricted to the most probable tokens.
4. Append the token to the input, update the hidden state with it, repeat until EOS.

> [!example]- Worked Example
> Prompt "I like". RNN predicts:
>
> | Word | Probability |
> |---|---|
> | natural | 0.25 |
> | machine | 0.18 |
> | to | 0.12 |
> | data | 0.09 |
>
> If "natural" is selected, the next step computes $p(w \mid \text{I, like, natural})$, and so on.

> [!warning] Common Misconception
> The model is not "remembering" the prompt — it is feeding the new token into its hidden state at each step. If the hidden state is reset, generation loses all prior context.

## Significance
Autoregressive generation is the inference template inherited by every modern language model, from RNNs to GPT. The decoding strategies (greedy / sampling / beam / top-k / top-p) are an architecture-independent toolkit for trading off fluency against diversity.
