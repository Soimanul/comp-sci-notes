**Tags:** #concept #llm
**Related:** [[Software 1.0 vs 2.0 Evolution]], [[Transformer Architecture]]

## Definition

**Transformers as State** describes the paradigm shift in how an AI system manages conversational context. In LLMs, the **context window** (the sequence of tokens the model can "see") replaces explicit state variables or database entries.

> [!info] Key Intuition
> In a traditional chatbot, "state" was a variable in a database: `currentStep = 3`, `userHasConfirmed = True`. In an LLM, "state" is implicit in the tokens: everything the user said and the model responded is concatenated in the prompt, and the model uses self-attention to extract what's relevant. There is no explicit state machine.

## Context Window as Memory

| Traditional System | LLM System |
|---|---|
| State stored in a database variable | State is the current context window tokens |
| Transitions follow hand-coded rules | Next token prediction from the full context |
| Limited to pre-defined paths | Handles any conversational path |
| State is explicit and auditable | State is implicit (distributed in activations) |

## Implications

- The **context window size** is the critical constraint: older or longer conversations may be truncated.
- Every token in the context counts toward cost and latency.
- **Long-context models** (Llama 3 at 128K tokens) extend how much "state" can be maintained.

> [!warning] Common Misconception
> LLMs do **not** have persistent memory by default. If the conversation exceeds the context window, older turns are dropped. Persistent memory requires external storage (RAG, vector databases) — see [[RAG Pipeline]].

## Significance

Understanding context-as-state is fundamental to designing LLM-based applications: system prompts, conversation history management, and context stuffing strategies all flow from this concept.
