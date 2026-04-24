**Tags:** #concept #llm
**Related:** [[Transformers as State]], [[Agentic Workflows]], [[LLM Evaluation]]

## Definition

**RAG (Retrieval-Augmented Generation)** is an architecture that solves the LLM knowledge cutoff and hallucination problem by **retrieving relevant external documents** and injecting them into the prompt before generation.

> [!info] Key Intuition
> LLMs are trained on data up to a cutoff date and cannot access private knowledge. RAG gives the model "open book access" — it looks up relevant facts and includes them in the prompt, so the model generates answers grounded in retrieved evidence rather than memorised training data.

## The RAG Pipeline (4 Steps)

### 1. Ingestion
`Document → Chunking → Embedding → Vector Store`
- Split documents into chunks.
- Embed each chunk using a sentence embedding model.
- Store embeddings in a vector database (ChromaDB, Pinecone, pgvector).

### 2. Retrieval
`User Query → Vector Search → Top-K Relevant Chunks`
- Embed the user's query.
- Search the vector store for the most similar chunks (cosine similarity or ANN search).
- Retrieve the top-K most relevant passages.

### 3. Augmentation
Inject retrieved text into the **system prompt**: "Answer only using the following context: {retrieved chunks}"

### 4. Generation
The LLM generates a response based only on the provided context — grounded in retrieved evidence.

## Key Challenges

> [!warning] Key Insight
> **Garbage In, Garbage Out.** Embedding quality and chunking strategy are more important than the LLM choice. A bad chunking strategy that splits a sentence across two chunks will cause retrieval failures even with a state-of-the-art LLM.

## Tech Stack

| Component | Tools |
|---|---|
| Orchestration | LangChain, LlamaIndex |
| Vector DBs (local) | ChromaDB |
| Vector DBs (cloud) | Pinecone |
| Vector DBs (SQL) | pgvector |

> [!example]- Example
> A customer service bot trained until 2024 is asked about a product launched in 2025. Without RAG: hallucination. With RAG: the query retrieves the product spec from the company's internal knowledge base and the answer is accurate.

## Significance

RAG is the dominant pattern for deploying LLMs on private or up-to-date knowledge. It reduces hallucination, enables knowledge updates without retraining, and makes answers verifiable through citations.
