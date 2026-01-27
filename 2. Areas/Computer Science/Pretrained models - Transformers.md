**Tags:** #concept #nlp #python #transformers #pretrained-models  
**Related:** [[Python NLP Tooling Landscape]] · [[Embeddings]] · [[Library tradeoffs - control vs robustness]]

## Definition
Pretrained transformer models are large neural models trained on massive corpora and accessed through Python interfaces, providing strong language capabilities through reusable model checkpoints rather than hand-designed rules or task-specific feature engineering.

## What they provide
- General-purpose language representations (embeddings) and task-ready heads.
- High-level APIs that abstract tokenization, model execution, and decoding.

## Strengths
- High performance across many NLP tasks.
- Transfers well to new tasks with limited labeled data.

## Limitations
- Internal assumptions are implicit and difficult to interpret.
- Higher computational cost and operational complexity than classical methods.
- Requires managing model size, latency, and deployment constraints.
