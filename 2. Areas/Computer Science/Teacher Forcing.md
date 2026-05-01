**Tags:** #concept #training #nlp
**Related:** [[Encoder Decoder Architecture]], [[Sequence Language Modelling]], [[Recurrent Neural Networks]]

## Definition
Teacher forcing is a training strategy for autoregressive sequence models. At step $t$, the decoder is fed the **ground-truth** previous token $y_{t-1}$ rather than its own previous prediction $\hat{y}_{t-1}$.

> [!info] Key Intuition
> During training we cheat: we always feed the correct previous answer. This stabilises learning because errors don't compound, and it lets every decoder position be computed in parallel from the known target sequence.

## Mechanics
- Training input to the decoder at step $t$: the *true* token $y_{t-1}$ (right-shifted target sequence with a BOS at position 0).
- Loss: cross-entropy between the predicted distribution and the true $y_t$.
- Inference: no targets exist, so the decoder consumes its own previous outputs. This is the only way the two regimes differ.

> [!example]- Worked Example
> Target "I love cats". With teacher forcing the decoder sees:
> - step 1: input = BOS, predict "I"
> - step 2: input = "I" (truth), predict "love"
> - step 3: input = "love" (truth), predict "cats"
>
> Even if the model wrongly predicted "hate" at step 2, step 3 still receives the correct "love" — errors do not compound.

## Trade-Off: Exposure Bias
Because the model never trains on its own (potentially wrong) outputs, the inference-time distribution of inputs differs from training. Errors at one step can drag generation off-distribution. Mitigations:
- **Scheduled sampling**: occasionally feed the model's own predictions during training.
- **Sequence-level losses** (REINFORCE, minimum risk training).
- **Large pretraining** can paper over the issue empirically.

> [!warning] Common Misconception
> Teacher forcing is not specific to Transformers — it is the default for any RNN, LSTM, or Transformer decoder trained on sequence prediction. Without it, parallel computation of decoder states during training would be impossible.

## Significance
Teacher forcing is the unsung hero behind fast and stable seq2seq training. Every encoder–decoder model in production uses it; understanding its limitation (exposure bias) is essential when models behave well in evaluation but drift during long generations.
