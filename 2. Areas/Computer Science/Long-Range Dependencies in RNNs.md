**Tags:** #concept #neural-networks #nlp
**Related:** [[Recurrent Neural Networks]], [[Vanishing and Exploding Gradients]], [[Hidden State (RNN)]]

## Definition
A long-range dependency is a relationship between tokens separated by many intermediate steps in a sequence. RNNs theoretically can model arbitrarily long contexts, but empirically simple RNNs only carry useful information across roughly 5–10 tokens.

> [!info] Key Intuition
> The hidden state has a finite capacity and is overwritten at every step. Without explicit gating, distant tokens get blurred away long before they reach the prediction.

## Why Simple RNNs Struggle

- **Gradient pathology**: BPTT multiplies by the recurrent matrix $W$ at every step. Singular values $< 1$ make gradients vanish exponentially in time, so distant tokens contribute almost nothing to the parameter update.
- **Uniform compression**: every token is treated identically. The model cannot decide that some tokens deserve more weight in the hidden state than others.

> [!example]- Worked Example
> "The book that I bought yesterday because the reviews were excellent **was** expensive."
>
> To predict "was", the model must remember that the subject is "book" — but many tokens lie between them. A vanilla RNN's hidden state has typically forgotten "book" by the time it reaches "was".

## Consequences
- The language model relies mostly on the most recent tokens.
- Training data far from the next-token target contributes weakly to the gradient signal.
- Practical context length is limited even when the architecture allows arbitrary inputs.

## What Helps
- **Gating** (LSTM, GRU): selective memory that resists overwriting.
- **Attention / Transformers**: direct token-to-token connections, no information bottleneck through a single hidden state.
- **Residual / skip connections**: shortcut paths for gradients.

## Significance
The inability of vanilla RNNs to capture long-range dependencies is the historical motivation for LSTMs, GRUs, and ultimately attention-based models. Most progress in sequence modelling can be read as progress on this single problem.
