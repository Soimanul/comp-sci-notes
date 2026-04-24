**Tags:** #concept #ml #nlp
**Related:** [[Pretraining in NLP]], [[Fine-tuning in NLP]], [[Zero-Shot Learning]], [[BERT]]

## Definition

**Transfer learning** is the practice of applying a model trained on one large task or dataset to a different (usually smaller) target task, rather than training from scratch. In NLP, this means pre-training a language model on a massive text corpus, then fine-tuning on a specific downstream task.

> [!info] Key Intuition
> Training a model from scratch on a small labelled dataset is data-inefficient — the model must learn both general language understanding and the task-specific pattern simultaneously. Transfer learning separates these: pre-train general understanding on billions of words, then specialise on hundreds or thousands of labelled examples.

## Why It Works

Language models pre-trained on large corpora learn:
- Syntax and grammar (word order, dependencies)
- Semantics (word meaning, coreference)
- World knowledge (facts encoded in text)
- Discourse structure

These representations transfer directly to downstream tasks (sentiment, NER, QA) because those tasks also require language understanding.

## Transfer Learning Pipeline

```
Large unlabelled corpus
        ↓
  Pre-training (self-supervised)
        ↓
  Pre-trained model (e.g. BERT, GPT)
        ↓
  Fine-tuning on labelled task data
        ↓
  Task-specific model
```

## Degrees of Transfer

| Approach | Description | Labelled data needed |
|---|---|---|
| Zero-shot | Apply pre-trained model directly, no task-specific training | None |
| Few-shot | Show model a handful of examples in context | Very few (in-context) |
| Fine-tuning | Train all or subset of weights on labelled data | Hundreds–thousands |
| Feature extraction | Freeze weights; use representations as features | Hundreds–thousands |

## Significance

Transfer learning reduced the data requirements for NLP by orders of magnitude and achieved state-of-the-art results across all GLUE/SuperGLUE benchmarks. It is the standard approach for virtually all production NLP systems.
