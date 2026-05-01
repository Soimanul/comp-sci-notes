**Tags:** #topic #hub #nlp
**Related:** [[Beyond Vanilla RNNs]], [[Transformer Architecture]], [[Natural Language Processing]]

## Overview
This hub follows the path from Bahdanau-style attention bolted onto an RNN encoder–decoder to the fully attention-based Transformer. It introduces the Query/Key/Value abstraction, cross-attention, masked (causal) self-attention, teacher forcing, and the major architectural variants — encoder-only (BERT), decoder-only (GPT), and encoder–decoder (BART).

> [!abstract]- TL;DR
> Attention turns the encoder's hidden states into a key–value store that the decoder queries dynamically; replacing the recurrence inside encoder and decoder with self-attention yields the Transformer. The same building blocks — self-attention and cross-attention — give rise to the encoder-only, decoder-only, and encoder–decoder model families.

## Knowledge Map

### 1. Attention on Top of RNNs
- [[Bahdanau Attention]]
- [[Keys Queries Values]]
- [[Teacher Forcing]]

### 2. Attention Without Recurrence
- [[Self-Attention]]
- [[Cross-Attention]]
- [[Masked Self-Attention]]

### 3. The Transformer Stack
- [[Transformer Architecture]]
- [[Multi-Head Self-Attention]]
- [[Positional Encoding]]
- [[Residual Connections]]
- [[Layer Normalization]]

### 4. The Family of Models
- [[Transformer Family]]
- [[BERT]]
- [[ChatGPT]]

> [!question]- Common Exam Questions
> - Explain the database analogy: what plays the role of keys, queries, and values in classical attention?
> - Why does the decoder need a causal mask in self-attention?
> - How do BERT, GPT, and BART differ at the architectural level, and which tasks suit each?
> - What changes between encoder self-attention and decoder cross-attention?
