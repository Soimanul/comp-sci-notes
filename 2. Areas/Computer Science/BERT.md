**Tags:** #concept #nlp #dl
**Related:** [[Transformer Architecture]], [[Pretraining in NLP]], [[Fine-tuning in NLP]], [[Self-Attention]], [[Multi-Head Self-Attention]], [[RLHF]]

## Definition

**BERT (Bidirectional Encoder Representations from Transformers)** is a pre-trained Transformer **encoder** that builds deeply contextualised word representations by attending to both left and right context simultaneously, pre-trained on masked language modelling (MLM) and next sentence prediction (NSP).

> [!info] Key Intuition
> GPT reads left-to-right. BERT reads all tokens at once, attending in both directions. This bidirectionality lets BERT build much richer contextual representations — "bank" in "river bank" and "bank account" get different vectors in BERT, based on full context.

## Architecture

- **Transformer encoder** stack (no decoder)
- BERT-base: 12 layers, 12 heads, $d_{model} = 768$, 110M parameters
- BERT-large: 24 layers, 16 heads, $d_{model} = 1024$, 340M parameters

## Special Tokens

- `[CLS]`: prepended to every input; its final hidden state is used for classification
- `[SEP]`: separates two sentences (used for NSP and sentence-pair tasks)
- `[MASK]`: replaces tokens during MLM pre-training

## Pre-training Objectives

### Masked Language Model (MLM)
Randomly mask 15% of tokens → predict them from context:
$$P(w_{\text{mask}} | w_1, \ldots, w_{T})$$

### Next Sentence Prediction (NSP)
Given sentence A and B, predict if B follows A in the corpus (50% true/50% random).

## Input Representation

$$\text{input} = \text{Token Embedding} + \text{Segment Embedding} + \text{Position Embedding}$$

## Fine-tuning for Tasks

| Task | Modification |
|---|---|
| Classification | Linear on [CLS] |
| NER / POS | Linear on each token |
| SQuAD QA | Two linear layers → start/end span |
| Sentence similarity | Linear on [CLS] with sentence pair input |

> [!warning] BERT vs. GPT
> BERT (encoder-only) is excellent for understanding tasks (classification, NER, QA). GPT (decoder-only) is designed for generation. For tasks requiring both understanding and generation, use encoder-decoder models (T5, BART) or instruction-tuned LLMs.

## Significance

BERT (Devlin et al., 2018) achieved state-of-the-art on 11 NLP benchmarks upon release and established the pre-train → fine-tune paradigm as the standard for NLP. Virtually all modern NLP systems trace back to BERT's design decisions.
