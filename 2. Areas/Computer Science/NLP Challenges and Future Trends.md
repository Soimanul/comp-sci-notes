**Tags:** #topic #hub #nlp
**Related:** [[Natural Language Processing]], [[Attention to Transformer]]

## Overview
This hub takes a step back from individual architectures and looks at how a single Transformer underwrites virtually every NLP task — classification, QA, summarisation — through prompt formulation rather than through different models. It then examines the limitations that follow (static internal knowledge, finite context window) and the responses to those limitations (retrieval-augmented generation, large context models, agentic loops).

> [!abstract]- TL;DR
> A Transformer always does the same thing — predict the next token. Tasks differ only in how we structure the input and interpret the output. RAG, larger context windows, and agentic loops are responses to the static-knowledge and finite-context limits of this single mechanism.

## Knowledge Map

### 1. The Unified View
- [[Tasks as Generation]]

### 2. Limits of Internal Knowledge
- [[RAG Pipeline]]

### 3. Limits of Context
- [[Context Window Limitations]]
- [[Large Context Models]]

### 4. Beyond Single Forward Passes
- [[Agentic Workflows]]

> [!question]- Common Exam Questions
> - In what sense does a Transformer "do the same thing" for classification, QA, and summarisation?
> - What problem does retrieval-augmented generation solve, and what does it leave unsolved?
> - Why does enlarging the context window have diminishing returns on attention quality?
> - What is the qualitative shift between a single LLM call and an agentic loop?
