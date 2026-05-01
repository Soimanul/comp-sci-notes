**Tags:** #concept #nlp #neural-networks
**Related:** [[Encoder Decoder Architecture]], [[Attention Mechanism]], [[Long-Range Dependencies in RNNs]]

## Definition
In a vanilla encoder–decoder, the encoder must compress the *entire* input sequence into a single fixed-size vector (the final hidden state), which the decoder uses as context. This forced compression is the **information bottleneck**: as input length grows, the vector cannot hold all the relevant content, and translation/generation quality degrades.

> [!info] Key Intuition
> Asking one fixed-length vector to encode a 5-word sentence and a 50-word paragraph equally well is asking the impossible. The bottleneck is structural, not a training failure.

## Failure Modes
- **Compression problem**: hidden states have fixed length (typically 512–4096), but inputs can be arbitrarily long.
- **Forgetting problem**: each recurrent update blends old and new information; early tokens fade by the end of the sequence.
- **Unequal token contribution**: later tokens dominate the final state; words at the start of long sentences may be effectively absent from the context vector.

> [!example]- Worked Example
> Translating a 60-word German sentence to English: by the time the encoder has processed word 60, the contribution of words 1–10 has been overwritten dozens of times. The decoder, given only the final hidden state, has at best a blurred memory of the sentence's beginning.

## Why Gating Doesn't Solve It
Gated cells (LSTM, GRU) help the encoder *retain* information longer, but the bottleneck is not just about retention — it is about the decoder having to read the entire input through a single vector. Gating slows the decay; it does not change the geometry.

> [!warning] Common Misconception
> The bottleneck is sometimes blamed on RNNs in general. Replacing an RNN with another sequential encoder leaves the bottleneck intact as long as the decoder still receives only one summary vector.

## The Fix
Attention removes the bottleneck by giving the decoder access to *all* encoder hidden states and learning, at every decoding step, which ones to attend to. Memory becomes selective access rather than fixed-size storage.

## Significance
The information bottleneck is the precise reason attention was invented (Bahdanau et al., 2014). Understanding it explains both why pre-attention NMT plateaued and why attention's improvement was so dramatic.
