**Tags:** #topic #hub #nlp
**Related:** [[Recurrent Neural Networks]], [[Natural Language Processing]]

## Overview
Vanilla RNNs collapse under long sequences due to vanishing gradients and a single fixed-size hidden state. This hub follows the architectural arc that fixes both: gating (LSTM, GRU) stabilises memory inside the cell; encoder–decoder separates representation from generation; the information bottleneck of a single context vector then motivates the attention mechanism.

> [!abstract]- TL;DR
> Gating turns the recurrent cell into a controlled memory (LSTM, GRU). Encoder–decoder networks separate sequence representation from generation but compress everything into one vector — an information bottleneck that attention is invented to break.

## Knowledge Map

### 1. The Gating Idea
- [[Gating Mechanism]]
- [[LSTM]]
- [[GRU]]

### 2. Sequence-to-Sequence Models
- [[Encoder Decoder Architecture]]
- [[Information Bottleneck (Encoder-Decoder)]]

### 3. From Memory to Selective Access
- [[Attention Mechanism]]

> [!question]- Common Exam Questions
> - How does a gate stop information from being overwritten in a recurrent cell?
> - Compare LSTM and GRU: what does GRU drop, and what does it gain?
> - Why does the encoder in an encoder–decoder system not have its own loss?
> - What concretely is the information bottleneck and how does attention remove it?
