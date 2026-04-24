**Tags:** #concept #nlp #dl
**Related:** [[Transfer Learning]], [[Fine-tuning in NLP]], [[BERT]], [[Modern NLP Approaches]]

## Definition

**Pre-training in NLP** is the process of training a large neural network on a massive, self-supervised text objective (no human labels needed) to learn general language representations that can be transferred to downstream tasks.

> [!info] Key Intuition
> The web contains trillions of words of human-written text — far more than any labelled task. Pre-training leverages this abundance: instead of supervised labels, use the text itself as supervision (predict masked words, predict the next word).

## Pre-training Objectives

| Objective | Description | Model |
|---|---|---|
| **Causal LM (CLM)** | Predict next token given left context: $P(w_t \| w_{<t})$ | GPT-1/2/3 |
| **Masked LM (MLM)** | Predict randomly masked tokens given full context | BERT |
| **Next Sentence Prediction (NSP)** | Predict if sentence B follows sentence A | BERT |
| **Sentence Order Prediction (SOP)** | Predict if sentence pair is in correct order | ALBERT |
| **Text-to-text** | Reconstruct corrupted text spans | T5 |

## BERT Pre-training Details (MLM)

- Randomly mask 15% of tokens
- 80% → replace with [MASK]
- 10% → replace with random token
- 10% → keep unchanged
- Train to predict the original token at masked positions

This forces the model to build bidirectional contextual representations.

## Data Scale

| Model | Pre-training data |
|---|---|
| BERT | BookCorpus + Wikipedia (~16GB) |
| GPT-3 | CommonCrawl + books + Wikipedia (~570GB) |
| LLaMA 2 | ~2 trillion tokens |

## Significance

Pre-training is what makes modern NLP work. The representations learned during pre-training capture linguistic and world knowledge that dramatically reduces the labelled data needed for any downstream task. It is the "foundation" of foundation models.
