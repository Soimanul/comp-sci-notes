**Tags:** #concept #llm
**Related:** [[RLHF]], [[Agentic Workflows]], [[RAG Pipeline]]

## Definition

**Memory in LLMs** refers to the different mechanisms by which an LLM-based system can store and retrieve information beyond what is in the base model weights — essential for building stateful agents and chatbots that maintain context across interactions.

> [!info] Key Intuition
> A base LLM has only **parametric memory** (knowledge baked into weights during pre-training). For applications requiring conversation history, personal preferences, or access to external knowledge, explicit memory mechanisms must be added.

## Four Types of Memory

### 1. In-Context Memory (Working Memory)
- The model's **context window** (input tokens)
- Temporary: cleared at the end of the conversation
- Limited by context length (4K–1M tokens depending on model)
- Usage: conversation history, retrieved documents, few-shot examples

### 2. External Memory (Episodic/Semantic)
- Vector databases or traditional databases accessed via retrieval
- Persistent across sessions
- Scales to billions of facts
- Usage: [[RAG Pipeline]] (retrieved documents), personal memory stores, knowledge bases

### 3. Parametric Memory (Long-term)
- Information encoded in model **weights** during training/fine-tuning
- Cannot be updated at inference time
- Usage: general world knowledge, language understanding

### 4. Cache Memory (Computational)
- [[KV Caching]]: cached key-value tensors from previous tokens
- Speeds up inference by avoiding recomputation
- Not semantic memory; purely computational

## Memory Comparison

| Type | Persistence | Capacity | Update at inference |
|---|---|---|---|
| In-context | Session | Context window | Yes (by adding tokens) |
| External | Permanent | Unlimited | Yes (via retrieval) |
| Parametric | Permanent | ~100B parameters | No (requires training) |
| Cache (KV) | Request | GPU memory | Automatic |

> [!example]- Chatbot Memory Design
> A production chatbot might use: (1) in-context for the last 10 turns; (2) external DB for user profile/history; (3) RAG for product catalogue lookup; (4) KV cache for inference speed.

## Significance

Memory management is one of the core engineering challenges in building LLM-based applications. The choice of memory type directly affects the system's ability to personalise, maintain coherence, and access up-to-date information.
