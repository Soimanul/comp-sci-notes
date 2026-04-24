**Tags:** #hub #llm
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> RLHF (Reinforcement Learning from Human Feedback) aligns LLMs with human preferences by first training a reward model on human comparison data, then fine-tuning the LLM with PPO to maximise that reward. This is how ChatGPT-style instruction following is achieved. LLMs also require explicit memory management since their context window is finite.

## Overview

Raw pre-trained LLMs follow the text distribution of the training corpus, not human preferences. RLHF is the key alignment technique that turns a pre-trained base model into a helpful, harmless, and honest assistant.

## Knowledge Map

- [[RLHF]]
- [[RLHF vs Cross-Entropy Training]]
- [[Memory in LLMs]]

> [!question]- Exam Questions
> - Describe the three stages of the RLHF pipeline.
> - How is the reward model trained in RLHF?
> - Why is RLHF more effective than supervised fine-tuning alone for instruction following?
> - What is the KL penalty term in the RLHF objective and why is it necessary?
> - What are the four types of memory available to an LLM-based agent?
