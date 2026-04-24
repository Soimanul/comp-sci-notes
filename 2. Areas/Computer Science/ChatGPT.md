**Tags:** #concept #llm #chatbot
**Related:** [[RLHF]], [[OpenAI Chat Completion API]], [[Evolution of Chatbots]]

## Definition

**ChatGPT** is OpenAI's conversational AI product (released November 2022), built on GPT-3.5 and later GPT-4 models fine-tuned with **RLHF** to follow instructions and engage in helpful, coherent multi-turn conversations.

> [!info] Key Intuition
> ChatGPT = pre-trained GPT + Supervised Fine-Tuning (SFT) on demonstrations + Reward Model trained on human preferences + PPO alignment. The result is a general-purpose assistant that can write code, explain concepts, draft documents, and answer questions across virtually all domains.

## Technical Foundation

| Component | Description |
|---|---|
| Base model | GPT-3.5 (davinci-002), later GPT-4 |
| Pre-training | Next-token prediction on ~570GB of text (GPT-3) |
| SFT | Human demonstration conversations |
| Reward model | Trained on human pairwise preference rankings |
| RL alignment | PPO optimising reward minus KL penalty |

## ChatGPT Capabilities

- Multi-turn conversation with context maintained in the message history
- Code generation, debugging, and explanation
- Text summarisation, translation, classification
- Structured output (JSON, tables, lists)
- Instruction following in multiple languages

## Limitations

| Limitation | Description |
|---|---|
| Knowledge cutoff | Training data has a date cutoff; cannot access real-time information |
| Hallucination | Can confidently generate plausible-sounding false information |
| Context window | Cannot process documents exceeding the context limit |
| Reasoning errors | Fails on complex multi-step mathematical or logical reasoning |

## Versions

| Version | Context | Key features |
|---|---|---|
| GPT-3.5-turbo | 4K–16K tokens | Original ChatGPT; fast and cheap |
| GPT-4 | 8K–128K tokens | Stronger reasoning; multimodal |
| GPT-4o | 128K tokens | Multimodal (text+image+audio); faster |
| o1/o3 | Long | Chain-of-thought reasoning |

## Significance

ChatGPT's release triggered mass adoption of LLMs and established the conversational AI interface as the primary way users interact with AI systems. It directly motivated competing products (Claude, Gemini, Llama) and a new field of LLM engineering.
