**Tags:** #concept #nlp #ner #transformers
**Related:** [[Named Entity Recognition]], [[CRF for Sequence Labelling]], [[BIO Tagging Scheme]]

## Definition

BERT-based NER fine-tunes a pretrained BERT encoder for token classification by adding a linear classification head over each token's contextual representation, optionally followed by a CRF layer. It achieves state-of-the-art NER by leveraging deep bidirectional context from pretraining.

> [!info] Key Intuition
> BERT already "knows" that "Cook" in "Tim Cook visited Apple" refers to a person — contextual embeddings encode world-knowledge co-occurrence patterns learned from billions of tokens. Fine-tuning simply teaches the classifier to surface that signal as BIO labels.

## Core Mechanics

**Architecture**:
1. **Tokenisation** — WordPiece splits words into subword tokens; only the first subword of each word is used for classification (or all subwords are averaged)
2. **BERT encoder** — 12–24 transformer layers produce contextual representations $\mathbf{h}_i$ per token
3. **Linear head** — $\mathbf{W} \mathbf{h}_i + \mathbf{b}$ → scores over BIO tag set
4. **Optional CRF** — enforces tag transition constraints

**Fine-tuning**: train on labelled NER data (e.g., CoNLL-2003) with cross-entropy loss or CRF loss; update all BERT parameters.

> [!example]- Worked Example
> Input: *[CLS] "Google acquired DeepMind in 2014" [SEP]*
> BERT assigns contextual embeddings to each token. Fine-tuned head predicts:
> `O B-ORG O B-ORG I-ORG O O O`

## Significance

BERT-based systems pushed NER F1 above 93% on CoNLL-2003 English, compared to ~85–89% for BiLSTM-CRF systems, largely eliminating the need for manual feature engineering.
