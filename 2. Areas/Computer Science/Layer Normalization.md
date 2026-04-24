**Tags:** #concept #dl
**Related:** [[Transformer Architecture]], [[Residual Connections]]

## Definition

**Layer Normalisation (LayerNorm)** normalises the activations within a single training example across the **feature dimension** (not across the batch), stabilising training by controlling the mean and variance of each layer's output.

> [!info] Key Intuition
> Without normalisation, activations in deep networks can grow or shrink exponentially, causing gradient instability. LayerNorm keeps activations well-scaled at every layer, making optimisation smoother and deeper networks trainable.

## Formula

For an activation vector $x \in \mathbb{R}^d$ (one token's representation):

$$\text{LayerNorm}(x) = \gamma \odot \frac{x - \mu}{\sqrt{\sigma^2 + \epsilon}} + \beta$$

Where:
- $\mu = \frac{1}{d} \sum_{j=1}^d x_j$ — mean across features
- $\sigma^2 = \frac{1}{d} \sum_{j=1}^d (x_j - \mu)^2$ — variance across features
- $\gamma, \beta \in \mathbb{R}^d$ — learned scale and shift parameters
- $\epsilon$ — small constant for numerical stability (e.g. $10^{-8}$)

## Layer Norm vs. Batch Norm

| Property | Layer Norm | Batch Norm |
|---|---|---|
| Normalises over | Features (per example) | Batch (per feature) |
| Works with batch size 1 | Yes | No |
| Works with variable length | Yes | Difficult |
| Used in Transformers | Yes (standard) | Rarely |
| Inference = training | Yes | No (uses running stats) |

## Pre-LN vs. Post-LN

| Placement | Formula | Behaviour |
|---|---|---|
| **Post-LN** (original) | $y = \text{LN}(x + F(x))$ | Unstable for very deep models |
| **Pre-LN** (modern) | $y = x + F(\text{LN}(x))$ | More stable; used in GPT-2, LLaMA |

Most modern LLMs use Pre-LN (also called RMSNorm variant that omits the mean subtraction).

## Significance

Layer normalisation is an essential component of every Transformer block. Without it, training deep Transformers (12–100+ layers) is extremely unstable. Pre-LN placement has become the standard in modern LLMs for its improved training dynamics.
