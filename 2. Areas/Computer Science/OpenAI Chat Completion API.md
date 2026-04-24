**Tags:** #concept #llm
**Related:** [[ChatGPT]], [[OpenAI Responses API]], [[OpenAI Agents SDK]]

## Definition

The **OpenAI Chat Completion API** is a stateless REST API that accepts a list of messages (system, user, assistant) and returns a model-generated response. It is the foundational interface for building LLM-powered applications with OpenAI models.

> [!info] Key Intuition
> The API treats conversation as a structured JSON list of messages. The caller is responsible for maintaining the conversation history — the API itself is stateless (each request is independent). The model generates the next assistant message given the full message list.

## Request Structure

```json
{
  "model": "gpt-4o",
  "messages": [
    {"role": "system",    "content": "You are a helpful assistant."},
    {"role": "user",      "content": "What is matrix factorization?"},
    {"role": "assistant", "content": "Matrix factorization decomposes..."},
    {"role": "user",      "content": "How does ALS work?"}
  ],
  "temperature": 0.7,
  "max_tokens": 500
}
```

## Message Roles

| Role | Description |
|---|---|
| `system` | Sets the assistant's persona/instructions; not shown to users |
| `user` | The human's message |
| `assistant` | The model's previous responses (maintains history) |
| `tool` | Result from a function/tool call |

## Key Parameters

| Parameter | Description |
|---|---|
| `model` | Which model to use (gpt-4o, gpt-3.5-turbo, etc.) |
| `temperature` | Randomness: 0 = deterministic, 2 = very creative |
| `max_tokens` | Maximum tokens in the response |
| `stream` | If true, stream tokens as they are generated |
| `response_format` | `{"type": "json_object"}` for structured output |
| `tools` | List of function definitions the model can call |

## Stateless Nature

The API does not store conversation history. The caller must:
1. Store all messages locally
2. Append each new user message and assistant response
3. Send the full history with every request

This makes the caller responsible for context management and cost control (longer history = higher cost).

> [!warning] Context Window Limit
> The total tokens in `messages` + response must not exceed the model's context window. For long conversations, implement a summarisation or truncation strategy.

## Significance

The Chat Completion API is the most widely used LLM interface in the industry. Most LLM-powered applications (chatbots, coding assistants, document processors) are built directly on this API or compatible alternatives (Anthropic, Google, Azure).
