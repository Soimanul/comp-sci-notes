**Tags:** #concept #nlp #llm
**Related:** [[Transformer Architecture]], [[BERT]], [[ChatGPT]], [[Encoder Decoder Architecture]]

## Definition
The Transformer family is the set of architectures derived from the original encoder–decoder Transformer by keeping a subset of its components. Three canonical variants dominate NLP: encoder-only, decoder-only, and encoder–decoder.

> [!info] Key Intuition
> Same lego bricks, different builds. The choice of which blocks to keep — encoder, decoder, or both — directly determines whether the model is best at *understanding*, *generating*, or *transforming* sequences.

## The Three Variants

| Variant | Example | Components | Best At |
|---|---|---|---|
| Encoder-only | **BERT** (Google, 2018) | Bidirectional self-attention, masked language modelling | Classification, QA, sentence similarity |
| Decoder-only | **GPT** (OpenAI, 2018+) | Causal self-attention, next-token prediction | Generation, dialogue, code completion |
| Encoder–decoder | **BART** (Meta, 2020), T5 | Bidirectional encoder + autoregressive decoder + cross-attention | Summarisation, translation, paraphrasing |

## Why the Choice Matters
- **BERT**: every token sees full left+right context → rich representations, but no native left-to-right generation.
- **GPT**: every token sees only the past → natural generation, but cannot use right context for understanding.
- **BART/T5**: bidirectional understanding *plus* autoregressive generation → most flexible, at the cost of more parameters and complex training.

## Scale Snapshot
| Model | Stacks | Heads | Hidden | Params |
|---|---|---|---|---|
| BERT-base | 12 | 12 | 768 | 110M |
| GPT-3 | 96 | 96 | 12,288 | 175B |
| ViT-Huge | 32 | 16 | 1,280 | 632M |

> [!warning] Common Misconception
> GPT does not "understand" text in any semantic sense — its bidirectional analogue (BERT) is closer to producing representations one might call "understanding". GPT's coherence is statistical: the model has learned the conditional distribution of the next token, not the meaning of words.

## Significance
Knowing which variant fits a task saves both compute and engineering effort. Encoder-only for representations, decoder-only for chat/generation, encoder–decoder for transformations between sequences — this taxonomy is the practical decision tree behind almost every modern NLP system.
