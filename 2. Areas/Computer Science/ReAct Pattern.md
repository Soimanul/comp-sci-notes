**Tags:** #concept #llm
**Related:** [[Agentic Workflows]], [[Function Calling]]

## Definition

The **ReAct pattern** (Reason + Act) is a prompting strategy for agentic LLMs that interleaves **reasoning** steps with **action** steps, allowing the model to iteratively approach a goal with observable feedback.

> [!info] Key Intuition
> Instead of just acting blindly, the model thinks out loud before each action ("I need to check the order status"), then takes the action (call the API), then observes the result, then thinks again. This visible reasoning chain makes the agent more reliable and debuggable.

## The ReAct Cycle

```
Thought: "I need to find the user's order status."
Action: get_order_details(order_id="123")
Observation: "Order #123 was shipped yesterday via FedEx."
Thought: "I can now answer the user's question."
Final Answer: "Your order was shipped yesterday and should arrive soon."
```

The cycle repeats until the agent produces a final answer or hits a stopping condition.

## Why ReAct Over Pure Chain-of-Thought?

| Pure CoT | ReAct |
|---|---|
| Reasons only from model knowledge | Reasons + grounds in real-world tool outputs |
| Can hallucinate facts | Factual errors caught by tool observations |
| One-shot reasoning | Iterative, self-correcting reasoning |

> [!example]- Example Agent
> Task: "What is the current stock price of Apple and is it above its 52-week average?"
> Thought: I need to call a stock API for current price and 52-week data.
> Action: get_stock_data(ticker="AAPL")
> Observation: {current: $189, 52w_avg: $175}
> Thought: Current price $189 > 52w avg $175. I can answer.
> Answer: Yes, Apple is trading above its 52-week average.

## Significance

ReAct is the standard pattern in multi-step agentic systems and is implemented in major frameworks like LangChain and AutoGen. It enables LLMs to perform complex tasks that require accessing external data and making sequential decisions.
