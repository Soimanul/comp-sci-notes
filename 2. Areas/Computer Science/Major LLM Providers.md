**Tags:** #concept #llm
**Related:** [[ChatGPT]], [[OpenAI Chat Completion API]]

## Definition

**Major LLM providers** are the organisations offering large language models via API or open-source release for commercial and research use, each with flagship models and distinct positioning.

> [!info] Key Intuition
> The LLM landscape is competitive: multiple providers offer capable models with different trade-offs in capability, cost, context length, safety, and open-source availability. Knowing the landscape helps in selecting the right model for a given application.

## Primary Providers

### OpenAI
- **Flagship**: GPT-4o, o1/o3 (reasoning models)
- **Strengths**: Largest ecosystem, best instruction following, multimodal (text+image+audio)
- **API**: Chat Completions, Responses API, Agents SDK

### Anthropic
- **Flagship**: Claude 3.5 Sonnet, Claude 3 Opus
- **Strengths**: Safety-focused (Constitutional AI), long context (200K tokens), strong coding
- **API**: Messages API (compatible format to OpenAI)

### Google DeepMind
- **Flagship**: Gemini 2.0 Flash, Gemini 1.5 Pro
- **Strengths**: Very long context (1M tokens), multimodal, integrated with Google ecosystem
- **API**: Vertex AI, Google AI Studio

### Meta AI
- **Flagship**: LLaMA 3 (open weights)
- **Strengths**: Open-source; self-hostable; no API cost; active research community
- **Deployment**: Self-hosted or via Groq, Together AI, Hugging Face

### Mistral AI
- **Flagship**: Mistral Large, Mixtral 8x7B (MoE)
- **Strengths**: European provider; strong performance-to-cost; open-weights models
- **API**: La Plateforme

### Cohere
- **Flagship**: Command R+ (RAG-optimised)
- **Strengths**: Enterprise focus; strong retrieval-augmented generation; embeddings API
- **API**: Cohere API

## Selection Criteria

| Criterion | Best Choice |
|---|---|
| Best overall capability | GPT-4o, Claude 3.5 Sonnet |
| Lowest cost | GPT-3.5-turbo, Mistral 7B |
| Longest context | Gemini 1.5 Pro (1M), Claude 3 (200K) |
| Open-source / self-hosted | LLaMA 3, Mistral |
| RAG workloads | Cohere Command R+ |

## Significance

Provider selection affects cost, latency, capability, data privacy, and vendor lock-in. Most production systems maintain compatibility with multiple providers (using OpenAI-compatible APIs where possible) to hedge against rate limits and pricing changes.
