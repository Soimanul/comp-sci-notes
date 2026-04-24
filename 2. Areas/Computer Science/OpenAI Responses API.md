**Tags:** #concept #llm
**Related:** [[OpenAI Chat Completion API]], [[OpenAI Agents SDK]], [[Agentic Workflows]], [[Memory in LLMs]]

## Definition

The **OpenAI Responses API** is a stateful, higher-level API (successor to the Chat Completion API) that adds **built-in tool support** (web search, file search, code interpreter), **persistent conversation state management**, and **multi-turn context** handled server-side, simplifying agentic application development.

> [!info] Key Intuition
> The Chat Completion API is stateless — you manage history. The Responses API is stateful — OpenAI manages the conversation thread. It also bakes in common agentic tools (search, code execution) so developers don't need to build them manually.

## Key Differences from Chat Completion API

| Feature | Chat Completion API | Responses API |
|---|---|---|
| State management | Caller-managed | Server-managed (conversation threads) |
| Built-in tools | No | Web search, file search, code interpreter |
| Turn tracking | Manual | Automatic |
| Structured outputs | Via `response_format` | Native |
| Stream events | Token stream | Richer event stream |

## Built-in Tools

| Tool | Description |
|---|---|
| **Web search** | Model can query the web for up-to-date information |
| **File search** | Search over uploaded documents (vector store) |
| **Code interpreter** | Execute Python code in a sandboxed environment |

## Request Structure (simplified)

```json
{
  "model": "gpt-4o",
  "input": "Summarise the uploaded document",
  "tools": [{"type": "file_search"}],
  "store": true
}
```

## Thread Management

- Create a **thread** once; all subsequent turns reference the thread ID
- Previous messages are stored and retrieved automatically
- Eliminates the need to re-send full conversation history

> [!warning] Pricing
> The Responses API charges for both input tokens and **stored thread tokens**. Long-running assistants with large context accumulate significant storage costs.

## Significance

The Responses API reduces the boilerplate required to build production chatbots and assistants. It is the foundation of OpenAI's Assistants product and simplifies building document QA, code assistants, and agentic workflows.
