**Tags:** #concept #llm
**Related:** [[RAG Pipeline]], [[LLM Guardrails]], [[Agentic Workflows]]

## Definition

**LLM evaluation** is the process of measuring the quality, reliability, and safety of LLM outputs — a challenging problem because LLMs are stochastic and their outputs are often open-ended text.

> [!info] Key Intuition
> You cannot unit-test an LLM the same way you test a deterministic function. A prompt may generate different outputs on different runs, and "correct" is often subjective. Evaluation requires specialised techniques beyond standard ML metrics.

## Key Evaluation Metrics

| Metric | Definition |
|---|---|
| **Faithfulness** | Does the answer match the retrieved context? (Checks for hallucination) |
| **Answer Relevance** | Does the answer actually address the user's prompt? |
| **Context Precision** | Are the retrieved documents relevant to the question? |
| **Completeness** | Does the answer address all aspects of the question? |

## LLM-as-a-Judge

A common approach: use a **superior model** (e.g., GPT-4o) to evaluate the outputs of a smaller model by scoring them on accuracy, tone, safety, and relevance.

**Advantages**: Scalable; can evaluate open-ended text.
**Limitations**: The judge model has its own biases; cannot guarantee ground truth.

> [!warning] Common Misconception
> There is no single "accuracy" metric for LLM quality. Different tasks require different metrics: a chatbot's empathy is measured differently from a code generation model's correctness (which can be run and verified).

## Significance

Without reliable evaluation, you cannot measure improvement, detect regressions, or verify safety. LLM evaluation is an active research area and a critical engineering discipline for production AI systems.
