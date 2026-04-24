**Tags:** #concept #llm
**Related:** [[Agentic Workflows]], [[ReAct Pattern]]

## Definition

**Function calling** is the mechanism by which an LLM **identifies when it needs an external tool** and outputs a structured (JSON) payload to trigger that tool, rather than answering from its own knowledge.

> [!info] Key Intuition
> The LLM acts as an intelligent dispatcher: given a user query, it decides "I can't answer this from memory, but if I call `get_weather(location='London')` I'll have the data I need." It outputs structured JSON describing the function call, and the runtime executes it and returns the result to the model.

## How It Works

1. Developer defines available tools (functions) with schemas (name, description, parameters).
2. User sends a message.
3. LLM outputs **structured JSON** describing which function to call and with what arguments.
4. Runtime executes the function and returns the result.
5. Result is appended to the conversation; LLM generates the final response.

> [!example]- Example (OpenAI Responses API)
> ```python
> tools=[{"type": "function",
>   "function": {
>     "name": "getCurrentWeather",
>     "description": "Get the weather in location",
>     "parameters": {
>       "properties": {
>         "location": {"type": "string"},
>         "unit": {"type": "string", "enum": ["c", "f"]}
>       }, "required": ["location"]
>     }
>   }
> }]
> ```
> When user asks "What's the weather in London?", the LLM outputs: `{"name": "getCurrentWeather", "arguments": {"location": "London", "unit": "c"}}`.

## Significance

Function calling transforms LLMs from knowledge retrieval systems into **action-taking agents**. It enables integration with databases, APIs, code executors, and any external system — which is the foundation of all agentic applications.
