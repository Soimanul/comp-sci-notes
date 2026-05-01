**Tags:** #concept #nlp #neural-networks
**Related:** [[Attention Mechanism]], [[Self-Attention]], [[Encoder Decoder Architecture]], [[Transformer Architecture]]

## Definition
Cross-attention is the attention layer in an encoder–decoder Transformer where the queries come from one sequence (the decoder) and the keys and values come from another (the encoder output). It is the mechanism by which the decoder reads from the encoder.

$$Q = D \, W^Q, \quad K = E \, W^K, \quad V = E \, W^V$$
$$\mathrm{CrossAttn}(D, E) = \mathrm{softmax}\!\left(\frac{QK^\top}{\sqrt{d_k}}\right) V$$
where $D$ is the decoder's intermediate representation and $E$ is the encoder's output sequence.

> [!info] Key Intuition
> Cross-attention is how generation looks back at understanding. Self-attention contextualises within one sequence; cross-attention contextualises one sequence *with respect to another*.

## Where It Lives in the Transformer
Inside each decoder block, sandwiched between masked self-attention and the feed-forward network:
1. Masked self-attention over generated-so-far decoder tokens.
2. **Cross-attention** over the entire encoder output.
3. Position-wise feed-forward network.
4. Residual + layer norm around each.

> [!example]- Worked Example
> When translating "The transformers are great!" → "¡Los transformers son geniales!", and the decoder is currently producing "geniales", cross-attention learns weights peaked on the encoder positions of "great" (and probably "are"), pulling those features into the prediction.

> [!warning] Common Misconception
> Cross-attention is *not* masked. Each decoder position can attend to every encoder position freely — only the *self*-attention inside the decoder is masked to enforce autoregressive generation.

## Significance
Cross-attention is what makes the Transformer a true sequence-to-sequence model. Encoder-only models (BERT) lack it entirely; decoder-only models (GPT) lack it too. It is precisely what BART, T5, and translation Transformers add to combine understanding and generation.
