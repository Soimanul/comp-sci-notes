**Tags:** #concept #llm
**Related:** [[OpenAI Responses API]], [[Agentic Workflows]], [[ReAct Pattern]], [[Function Calling]]

## Definition

The **OpenAI Agents SDK** is an open-source Python framework for building multi-agent LLM applications, providing primitives for **agents** (LLMs with instructions and tools), **handoffs** (transferring control between agents), **guardrails** (input/output validation), and **tracing** (execution logging).

> [!info] Key Intuition
> Building a single-agent chatbot is straightforward. Building a system where a "triage agent" routes requests to a "billing agent" or a "technical support agent" — each with specialised tools and instructions — requires orchestration primitives. The Agents SDK provides these.

## Core Concepts

### Agent
An agent is an LLM configured with:
- A **model** (e.g. gpt-4o)
- **Instructions** (system prompt)
- **Tools** (functions the agent can call)
- Optional **handoffs** (other agents to transfer to)

```python
agent = Agent(
    name="Support Agent",
    instructions="Help users with technical issues.",
    tools=[search_kb, create_ticket],
    handoffs=[billing_agent]
)
```

### Handoffs
An agent can **hand off** a conversation to another agent when the task is outside its scope. The receiving agent gets the full conversation context.

### Guardrails
- **Input guardrails**: validate/transform user input before the agent processes it
- **Output guardrails**: validate/transform the agent's response before returning it
- Can block harmful content, enforce format requirements, apply PII redaction

### Tracing
Every agent run generates a trace (execution log) showing which agent ran, which tools were called, what inputs/outputs were produced — essential for debugging and evaluation.

## Execution Loop

```
User message
     ↓
Agent processes with LLM
     ↓
Tool call? → Execute tool → Return result → Continue
     ↓ (no tool or final answer)
Handoff? → Transfer to specialist agent
     ↓ (no handoff)
Return response to user
```

## Significance

The Agents SDK standardises the orchestration patterns (router, handoff, parallel agents) that previously required custom code. It enables rapid prototyping of multi-agent systems and integrates with OpenAI's tracing infrastructure for production monitoring.
