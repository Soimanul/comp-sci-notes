**Tags:** #concept #nlp
**Related:** [[Transformer Architecture]], [[BERT]], [[Transfer Learning]], [[Word Embeddings]]

## Definition

**Modern NLP approaches** refers to the paradigm shift from hand-crafted features and task-specific models to pre-trained neural language models (BERT, GPT, T5) that are fine-tuned on downstream tasks — achieving state-of-the-art performance across virtually all NLP benchmarks.

> [!info] Key Intuition
> The core insight is that most NLP tasks share the same underlying skill: understanding language. A model pre-trained to deeply understand language (via massive text corpora) needs only a small amount of task-specific data to excel at any specific task.

## Evolution of NLP Paradigms

| Era | Approach | Key Methods |
|---|---|---|
| Pre-neural | Feature engineering + shallow ML | TF-IDF, n-grams, SVMs, CRFs |
| Word vectors | Distributed word representations | Word2Vec, GloVe, fastText |
| Sequence models | Contextual representations | LSTM, ELMo, BiLSTM-CRF |
| Pre-trained LMs | Contextual embeddings + fine-tuning | BERT, GPT, RoBERTa, T5 |
| Foundation models | Instruction following, few-shot | ChatGPT, GPT-4, LLaMA |

## Key Shift: Context-Dependent Representations

**Static embeddings** (Word2Vec): "bank" always has the same vector — cannot distinguish "river bank" from "investment bank."

**Contextual embeddings** (BERT): "bank" has different representations in different sentences — the model reads the full context.

## Two Dominant Architectures

| Model type | Architecture | Training objective | Examples |
|---|---|---|---|
| Encoder-only | Transformer encoder | MLM (BERT) | BERT, RoBERTa, DistilBERT |
| Decoder-only | Transformer decoder | Next token prediction | GPT-3/4, LLaMA |
| Encoder-decoder | Full Transformer | Seq2Seq (T5) | T5, BART |

## Significance

Modern NLP approaches reduced the need for task-specific feature engineering and labelled data by 10–100×. BERT-based models are now the standard in production NLP systems (search, QA, NER, classification).
