**Tags:** #concept #nlp #dl
**Related:** [[Transfer Learning]], [[Pretraining in NLP]], [[BERT]], [[LoRA]]

## Definition

**Fine-tuning in NLP** is the process of taking a pre-trained language model and continuing training on a smaller, labelled, task-specific dataset to adapt the model's representations and output layer to the target task.

> [!info] Key Intuition
> The pre-trained model already "knows" language. Fine-tuning nudges the weights slightly so the model uses that knowledge to solve the specific task (e.g. classifying sentiment, extracting entities, answering questions). Relatively few gradient steps on small data are needed.

## Fine-tuning BERT

**Step 1: Add task head** (a linear layer on top of the pre-trained encoder):
- Classification: linear on [CLS] token output
- Token classification (NER, POS): linear on each token's output
- Question answering: two linear layers to predict start/end token positions

**Step 2: Train all parameters** end-to-end on labelled data (typically a few epochs, small learning rate ~2e-5).

```
Pre-trained BERT
      ↓
[CLS] token representation
      ↓
Linear layer (new weights)
      ↓
Task output
```

## Full Fine-tuning vs. Parameter-Efficient Fine-tuning

| Approach | Trainable params | Data needed | Cost |
|---|---|---|---|
| Full fine-tuning | All (110M–70B) | Thousands of examples | High compute |
| **LoRA** | Low-rank updates (~0.1%) | Thousands of examples | Low compute |
| **Adapters** | Bottleneck layers (~1%) | Thousands of examples | Medium |
| Prompt tuning | Soft prompt tokens only | Few examples | Very low |

> [!warning] Catastrophic Forgetting
> Full fine-tuning on a small dataset can cause **catastrophic forgetting**: the model overwrites general language knowledge with task-specific patterns. Mitigations: small learning rate, early stopping, regularisation (EWC), [[LoRA]].

## Practical Guidelines

- Learning rate: typically 1e-5 to 5e-5 (much smaller than pre-training)
- Epochs: 2–4 (more risks overfitting)
- Batch size: 16–32
- Warmup: 10% of training steps

## Significance

Fine-tuning enables a single pre-trained model (BERT, GPT) to achieve state-of-the-art on dozens of NLP tasks with minimal task-specific effort. It is the core deployment strategy for NLP in production.
