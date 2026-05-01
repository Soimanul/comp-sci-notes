**Tags:** #concept #neural-networks #nlp
**Related:** [[Recurrent Neural Networks]], [[Hidden State (RNN)]]

## Definition
RNNs can be wired into different input/output configurations depending on the task. The cell is the same — only the schedule of *when* to read inputs and *when* to emit outputs changes.

> [!info] Key Intuition
> An RNN is a flexible sequence transducer: by choosing where to plug inputs and where to read outputs, the same recurrent cell handles classification, generation, tagging, and translation.

## Configurations

| Configuration | Schedule | Example Task |
|---|---|---|
| **One-to-one** | Single input, single output (no recurrence really used) | Image classification |
| **Many-to-one** | Read full sequence, emit one label from final $h_T$ | Sentiment classification |
| **One-to-many** | Single input seeds the cell, then emit a sequence of outputs | Text generation from a prompt; image captioning |
| **Many-to-many (aligned)** | One output per input token | POS tagging, NER |
| **Many-to-many (unaligned)** | Encode input sequence, then decode output sequence of different length | Machine translation (encoder–decoder) |

> [!example]- Worked Example
> **Sentiment classification** is many-to-one: each token of the review is fed in turn into the same cell; only $h_T$ is passed to a feedforward classifier producing a positive/negative label.
>
> **POS tagging** is aligned many-to-many: at each step, the hidden state $h_t$ is mapped through an output layer to a tag for the corresponding token $x_t$.

> [!warning] Common Misconception
> Encoder–decoder is not a third architecture — it is two RNNs (or one shared cell used twice) glued by passing the encoder's final hidden state as the decoder's initial state. The classical machine translation setup is just two many-to-one + one-to-many components stitched together.

## Significance
Knowing the configuration vocabulary lets you pick the right wiring for a task without redesigning the cell. The same vocabulary is reused (with attention swapped for recurrence) in transformer-based models.
