**Tags:** #concept #llm
**Related:** [[Transformers as State]], [[RAG Pipeline]], [[Agentic Workflows]]

## Definition

The **evolution from Software 1.0 to 2.0** describes the paradigm shift in AI systems from hand-coded rules to learned probabilistic models, culminating in LLM-based systems where the entire context window becomes the state.

> [!info] Key Intuition
> Software 1.0 = "if user says X, do Y" (programmer-defined logic). Software 2.0 = "train a model on data to learn X → Y mappings automatically." LLMs represent a further shift: the model doesn't navigate a graph of states — it predicts the next token given everything in its context window.

## Three Eras

### Software 1.0: Rule-Based Era
- Logic defined by **hard-coded Finite State Machines (FSMs)** and regex.
- Strict intent classification: "If user says X, do Y."
- Chatbots were **decision trees** — every branch had to be hand-crafted.
- **Problem**: Fragile, unscalable, unable to handle nuance or context shifts.

### Software 2.0: Probabilistic Era
- Shift from "Programming" to "Training."
- The model learns to map inputs to outputs from data.
- Transformer architecture: leverages self-attention to weight the importance of different parts of input data.
- **Problem**: Still requires large labelled datasets; domain transfer is hard.

### Context as State (LLM Era)
- State is no longer a variable in a database — it is the **n tokens currently in the context window**.
- Predicting the next token vs. navigating a pre-defined graph.
- The model handles nuance, context shifts, and open-ended queries naturally.

> [!example]- Example Failure of Software 1.0
> Old chatbot: "I need to cancel my order" → matches "cancel" keyword → triggers cancellation flow. "My package arrived damaged and I'd like to return it and get my money back" → no match → fails. An LLM understands this is a refund request without explicit keyword matching.

## Significance

Understanding this evolution explains why modern chatbots are built on LLMs: the rule-based approach simply does not scale to the complexity and diversity of human language.
