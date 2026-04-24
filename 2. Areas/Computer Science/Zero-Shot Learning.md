**Tags:** #concept #ml #nlp
**Related:** [[Transfer Learning]], [[Fine-tuning in NLP]], [[BERT]]

## Definition

**Zero-shot learning** is the ability of a model to correctly perform a task on classes or tasks it has never explicitly been trained on, by generalising from other tasks or leveraging semantic knowledge embedded during pre-training.

> [!info] Key Intuition
> A model trained on many tasks sees "sentiment classification" and "entailment" during pre-training. At inference time, it can perform "toxicity detection" (never seen) by recognising it as a variant of what it has already learned — provided the task is described in natural language.

## Two Flavours in NLP

### 1. Zero-Shot Task Transfer (GPT-style)
The model is given a natural language task description with no examples:
```
Classify the sentiment of: "The food was terrible."
Answer:
```
GPT-3/4 can answer correctly without any sentiment-labelled training data.

### 2. Zero-Shot Class Transfer (Vision origins)
The model predicts classes not seen during training by leveraging semantic embeddings of class names. (More common in computer vision; in NLP usually called zero-shot prompting.)

## Zero-Shot vs. Few-Shot vs. Fine-tuning

| Approach | Examples in prompt | Weight update | Data needed |
|---|---|---|---|
| Zero-shot | 0 | No | None |
| Few-shot (in-context) | 1–10 | No | Very few |
| Fine-tuning | Hundreds+ | Yes (gradient descent) | Moderate |

## Why LLMs Excel at Zero-Shot

Large LLMs are exposed to enormous task diversity during pre-training (papers, books, code, Q&A forums). This implicitly trains multi-task capabilities. RLHF/instruction fine-tuning further aligns the model to follow natural language task descriptions without examples.

> [!example]- Zero-Shot NLI
> Premise: "The cat sat on the mat." Hypothesis: "There is a cat somewhere." Label: Entailment.
> Model (never trained on NLI) can classify this correctly via natural language understanding alone.

## Significance

Zero-shot capability is a key reason LLMs are transformative: they eliminate the data collection and labelling bottleneck for many NLP applications, enabling rapid prototyping and deployment of new NLP features.
