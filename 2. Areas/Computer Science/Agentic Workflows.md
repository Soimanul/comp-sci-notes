**Tags:** #concept #llm
**Related:** [[RAG Pipeline]], [[ReAct Pattern]], [[Function Calling]], [[LLM Guardrails]]

## Definition

**Agentic workflows** are LLM-based systems where the model does not just answer questions but **autonomously takes actions** — calling tools, querying APIs, running code, and iterating toward a goal.

> [!info] Key Intuition
> A chatbot answers. An agent *acts*. The agent loop: the LLM receives a task, decides what tool to use, observes the result, decides the next action, and repeats until the task is complete.

## Core Components

### The Agent Loop
An autonomous iteration where the model:
1. Receives a task or user message.
2. Reasons about what action to take.
3. Calls a tool (function, API, search, code executor).
4. Observes the tool's output.
5. Repeats until the goal is reached or it decides to respond.

*Example: Claude Code — given "fix the bug in this file", it reads the file, identifies the bug, writes a fix, runs tests, observes results, and iterates.*

### Function Calling
The mechanism by which an LLM identifies when it needs an external tool and outputs **structured data (JSON)** to trigger it. The function is then executed by the runtime and the result is fed back to the LLM.

See [[Function Calling]] for details.

### The ReAct Pattern
A specific agent reasoning pattern: **Reason + Act**. See [[ReAct Pattern]] for details.

## Significance

Agentic workflows transform LLMs from passive question-answerers into active problem-solvers. They are the foundation of modern AI assistants (GitHub Copilot, Claude Code, OpenAI Agents SDK) and are rapidly replacing traditional software automation.
