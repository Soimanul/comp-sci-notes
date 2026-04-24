**Tags:** #concept #dl #nlp
**Related:** [[Transformer Architecture]], [[Self-Attention]], [[Multi-Head Self-Attention]]

## Definition

**Positional encoding** injects information about the absolute or relative position of tokens into the Transformer input embeddings, since self-attention is **permutation-equivariant** — it treats the input as a set, not a sequence.

> [!info] Key Intuition
> Self-attention computes the same attention weights regardless of token order. Without positional encoding, "the dog bit the man" and "the man bit the dog" would produce identical representations. Positional encoding breaks this symmetry.

## Sinusoidal Positional Encoding (original Transformer)

For position $pos$ and dimension $i$:

$$PE_{(pos, 2i)} = \sin\left(\frac{pos}{10000^{2i/d_{model}}}\right)$$

$$PE_{(pos, 2i+1)} = \cos\left(\frac{pos}{10000^{2i/d_{model}}}\right)$$

- Even dimensions: sine waves of increasing period
- Odd dimensions: cosine waves of increasing period
- Periods range from $2\pi$ (dimension 0) to $20000\pi$ (dimension $d_{model}$)

The encoding is **added** to the token embedding: $x'_{pos} = x_{pos} + PE_{pos}$

## Properties of Sinusoidal Encoding

| Property | Description |
|---|---|
| Unique per position | Different pattern for each position |
| Relative positions | $PE_{pos+k}$ can be expressed as a linear function of $PE_{pos}$ |
| Generalises to unseen lengths | Deterministic formula works for any position |
| No learned parameters | Fixed at initialisation |

## Learned Positional Encoding (BERT, GPT)

BERT and GPT use **learned** positional embeddings: a lookup table of size $\text{max\_seq\_len} \times d_{model}$ trained with the model.

| Type | Advantage | Disadvantage |
|---|---|---|
| Sinusoidal | Extrapolates to longer sequences | Slightly inferior on benchmarks |
| Learned | Optimal for training distribution | Cannot extrapolate beyond training length |
| Relative (RoPE, ALiBi) | Models relative distances | More complex implementation |

## Significance

Positional encoding is what allows the Transformer to process ordered sequences. Without it, the architecture would be a bag-of-words model. The choice of positional encoding scheme significantly affects performance on long-context tasks ([[RoPE (Rotary Position Embedding)]] is now preferred in most modern LLMs).
