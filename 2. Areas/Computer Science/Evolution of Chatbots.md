**Tags:** #concept #chatbot
**Related:** [[ChatGPT]], [[RLHF]], [[The ELIZA Effect]], [[Turing Test]]

## Definition

The **evolution of chatbots** traces the progression from hand-coded rule-based systems through retrieval-based and generative ML approaches to modern LLM-based assistants, with each generation addressing the limitations of the previous.

## Generations

### Generation 1: Rule-Based (1960s–1990s)
- **Pattern matching**: ELIZA (1966), ALICE (AIML)
- Match user input to predefined patterns → fill in template responses
- Example: `"I feel *"` → `"Tell me more about feeling *."`
- **Limitation**: brittle, cannot handle novel phrasings, no real understanding

### Generation 2: Retrieval-Based (2000s–2015)
- Index a large corpus of (question, answer) pairs
- Retrieve the most similar question → return its answer
- Uses TF-IDF, BM25, or learned embeddings for matching
- **Limitation**: only returns existing responses, cannot generate novel answers

### Generation 3: Generative (2015–2020)
- Sequence-to-sequence models (Seq2Seq, attention): generate token-by-token responses
- Neural conversation models: trained on dialogue corpora
- **Limitation**: tendency for safe, generic responses ("I don't know"); no long-term coherence

### Generation 4: LLM-Based (2020–present)
- Large pre-trained Transformers + [[RLHF]] (ChatGPT, Claude, Gemini)
- General-purpose: instruction following, tool use, multi-turn coherence
- **Limitation**: hallucination, cost, latency

## Comparison

| Feature | Rule-Based | Retrieval | Generative | LLM |
|---|---|---|---|---|
| Novel responses | No | No | Yes | Yes |
| Factual accuracy | If coded correctly | High | Low | Moderate (hallucination risk) |
| Coherence | Yes (scripted) | Limited | Poor | Excellent |
| Personalisation | Hard-coded | Limited | Possible | Easy via prompt |

## Significance

Understanding this evolution explains why LLMs displaced earlier approaches and what problems remain open (hallucination, cost, safety). Each generation is still used in appropriate contexts — rule-based for FAQ bots, retrieval for search, LLMs for complex dialogue.
