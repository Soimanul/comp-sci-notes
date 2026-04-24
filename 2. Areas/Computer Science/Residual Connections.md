**Tags:** #concept #dl
**Related:** [[Transformer Architecture]], [[Layer Normalization]], [[Backpropagation]]

## Definition

**Residual connections** (skip connections) pass the input of a layer directly to its output by adding it to the layer's transformation: $\text{output} = F(x) + x$. This allows gradients to flow directly through the network during backpropagation, enabling training of very deep models.

> [!info] Key Intuition
> Without residual connections, training very deep networks suffers from vanishing/exploding gradients — the gradient signal degrades as it passes through many layers. With $F(x) + x$, the gradient has a direct path back to earlier layers through the identity shortcut.

## Formulation

In a Transformer block with residual connections:

$$y = \text{LayerNorm}(x + F(x))$$

where $F(x)$ is either:
- Multi-head self-attention: $F(x) = \text{MHA}(x)$
- Feed-forward network: $F(x) = \text{FFN}(x)$

## Why Residual Connections Work

**Gradient flow:** $\frac{\partial L}{\partial x} = \frac{\partial L}{\partial y} \cdot \frac{\partial (F(x) + x)}{\partial x} = \frac{\partial L}{\partial y}\left(\frac{\partial F(x)}{\partial x} + I\right)$

The $+I$ term ensures gradients are never zeroed out by a single layer, regardless of $\frac{\partial F(x)}{\partial x}$.

**Identity initialisation:** At initialisation, $F(x) \approx 0$ (small random weights), so the block approximates the identity. The network starts as a "shallow" model and learns depth incrementally.

## Usage in Transformers

Each Transformer block applies **two** residual connections:
1. Around the self-attention sub-layer: $x \leftarrow x + \text{MHA}(x)$
2. Around the feed-forward sub-layer: $x \leftarrow x + \text{FFN}(x)$

Both are followed by layer normalisation (Pre-LN or Post-LN depending on variant).

> [!example]- BERT Depth
> BERT-base has 12 encoder layers, BERT-large has 24. Without residual connections, training 24-layer Transformers would be extremely difficult. Residual connections make deep Transformers routinely trainable.

## Significance

Residual connections (He et al., 2015, ResNet) are one of the most important architectural innovations in deep learning, enabling networks with hundreds of layers. They are present in every modern Transformer and most deep CNN architectures.
