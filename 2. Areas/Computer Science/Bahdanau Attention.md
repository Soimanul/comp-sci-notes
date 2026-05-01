**Tags:** #concept #nlp #neural-networks
**Related:** [[Attention Mechanism]], [[Encoder Decoder Architecture]], [[Information Bottleneck (Encoder-Decoder)]]

## Definition
Bahdanau-style attention (additive attention) augments an RNN encoder–decoder so that, at every decoding step, the decoder dynamically constructs its context vector as a weighted sum of *all* encoder hidden states — not just the final one.

For a decoder state $s_t$ and encoder states $h_1, \dots, h_T$:
$$\text{score}_{ti} = s_t^\top h_i$$
$$\alpha_{ti} = \mathrm{softmax}_i\left(\text{score}_{ti}\right)$$
$$c_t = \sum_{i=1}^T \alpha_{ti} h_i$$
The output is then produced from $[s_t; c_t]$:
$$o_t = W_o [s_t; c_t] + b_o, \quad p_t = \mathrm{softmax}(o_t)$$

> [!info] Key Intuition
> The encoder no longer hands the decoder a single summary. It exposes its full sequence of states, and the decoder learns to focus on the right ones for each output step — translation no longer has to fit through a fixed-size pipe.

## Why It Was Invented
Vanilla encoder–decoder suffers from the information bottleneck: a single context vector cannot hold long sentences. Bahdanau et al. (2014) showed that letting the decoder peek at all encoder states removed this ceiling and dramatically improved long-sentence translation.

> [!example]- Worked Example
> Translating "The transformers are great!" → "¡Los transformers son geniales!". When the decoder is about to produce "Los", $\alpha_{t,i}$ peaks on the encoder state for "The" and on contextual neighbours like "transformers" (because "los" is a plural masculine article). When emitting "geniales", the weights shift to "great".

> [!warning] Common Misconception
> Bahdanau attention does *not* remove the recurrence — both encoder and decoder are still RNNs. It only changes how their hidden states are connected. Attention without recurrence is a separate later development (the Transformer).

## Significance
Bahdanau attention is the historical bridge between RNN-based NMT and Transformers. It introduced the core operation — a learned weighted lookup over a sequence of states — that the Transformer would later use everywhere.
