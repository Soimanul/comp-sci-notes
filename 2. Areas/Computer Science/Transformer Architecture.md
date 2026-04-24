**Tags:** #concept #dl #nlp
**Related:** [[Self-Attention]], [[Multi-Head Self-Attention]], [[Positional Encoding]], [[Residual Connections]], [[Layer Normalization]], [[BERT]]

## Definition

The **Transformer architecture** (Vaswani et al., 2017) is a sequence-to-sequence neural network that relies entirely on **self-attention** mechanisms (no recurrence, no convolution), enabling full parallelism during training and superior modelling of long-range dependencies.

> [!info] Key Intuition
> RNNs process tokens one at a time — token $t$ must wait for token $t-1$. The Transformer computes attention between all token pairs simultaneously, making it massively parallelisable on GPUs and able to directly model relationships between distant tokens.

## Architecture Overview

```
         Output probabilities
               ↑
        Linear + Softmax
               ↑
      ┌────────────────────┐
      │   Decoder Block ×N  │  (Cross-attention + Self-attention)
      └────────────────────┘
               ↑ (encoder output)
      ┌────────────────────┐
      │   Encoder Block ×N  │  (Self-attention + FFN)
      └────────────────────┘
               ↑
        Input Embeddings + Positional Encoding
```

## Encoder Block

Each encoder block contains:
1. **Multi-head self-attention**: each token attends to all other tokens
2. **Position-wise feed-forward network** (2-layer MLP per position)
3. **Residual connection + layer normalisation** around each sub-layer

## Decoder Block

Decoder blocks add:
1. **Masked self-attention**: each position can only attend to previous positions (causal)
2. **Cross-attention**: queries from decoder, keys/values from encoder output
3. **FFN** with residual + layer norm

## Key Equations

**Scaled dot-product attention:**
$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

The $\frac{1}{\sqrt{d_k}}$ scaling prevents softmax saturation in high-dimensional spaces.

## Significance

The Transformer is the foundation of virtually all modern NLP systems (BERT, GPT, T5, LLaMA) and has been extended to vision (ViT), audio (Whisper), and multimodal systems. Its parallelism made training on internet-scale data computationally feasible.
