# Git-Query: System Architecture & Engineering Report
**Date:** February 16, 2026
**Version:** 1.0 (Production Ready for 4.2M Scale)

---

## 1. Executive Summary
Git-Query is an AI-powered repository recommendation engine designed to scale to **4.2 million repositories**. It uses a **Hybrid Retrieval** strategy that combines the semantic understanding of Large Language Models (LLMs) with the precision of keyword search, refined by a deep-learning Reranker.

This document breaks down the system for a software engineer, detailing the architecture, the code structure, and the design patterns used.

---

## 2. High-Level Architecture

The system follows a **Microservices Architecture** using Docker containers.

### 2.1 Component Diagram

```mermaid
graph TD
    User[User / Frontend] -->|HTTP /recommend| Nginx[Nginx Gateway]
    Nginx -->|Proxy| API[Recommender API]
    
    subgraph "Data Plane"
        API -->|Semantic Search| Qdrant[Qdrant Vector DB]
        API -->|Keyword Search| Mongo[MongoDB (Metadata)]
        API -->|Cache| Redis[Redis Cache]
    end
    
    subgraph "ML Control Plane"
        Training[Training Service] -->|Writes Weights| SharedVol[Shared Volume]
        Training -->|Updates Status| Mongo
        API -->|Reads Weights| SharedVol
        API -->|Checks Status| Mongo
    end
```

### 2.2 Key Flows
1.  **Ingestion:** Data flows from Kaggle -> MongoDB (Metadata) -> Qdrant (Vectors).
2.  **Inference (Recommendation):**
    *   User Query -> **Hybrid Engine** -> (Vector Search + Text Search).
    *   Results merged via **RRF (Reciprocal Rank Fusion)**.
    *   Top 50 results -> **Cross-Encoder Reranker** -> Top 10 Results.
3.  **Training:**
    *   User Interactions (Clicks) -> **Training Pipeline** -> Fine-tuned Model.
    *   Model -> **Registry** -> Hot-swapped into Inference API.

---

## 3. Engineering Concepts & Patterns

### A. The Strategy Pattern (Engines)
**Where:** `src/recommender/engines/`
**Concept:** We define a common interface `RecommendationEngine`. The API doesn't know *how* recommendations are generated, it just calls `.recommend()`.
*   **Why?** This allows us to swap algorithms (e.g., "Baseline" vs "Hybrid") at runtime for A/B testing without changing the API code.

### B. Hybrid Retrieval (RRF)
**Where:** `src/recommender/engines/hybrid.py`
**Concept:** We run two searches in parallel:
1.  **Dense Retrieval (Vectors):** Finds "meaning" (e.g., "fast web server" finds "hurricane").
2.  **Sparse Retrieval (Keywords):** Finds exact matches (e.g., "react").
**Fusion:** We merge them using `score = 1 / (k + rank)`. This ensures that a repo appearing in *both* lists gets a huge boost, while preserving unique findings from each.

### C. The Model Registry Pattern
**Where:** `src/recommender/services/registry_service.py`
**Concept:** Decoupling the *creator* of a model (Training) from the *consumer* (API).
*   **Storage:** The binary files live on a shared disk.
*   **State:** The "Source of Truth" (which version is active?) lives in MongoDB.
*   **Why?** Allows zero-downtime updates. The API loads the new model into RAM before switching traffic to it.

---

## 4. Codebase Walkthrough (Deep Dive)

### `src/recommender/api.py`
**Role:** The Entry Point (Controller).
*   **`lifespan(app)`**: Handles startup. Connects to DBs and loads the initial "Active" models into memory.
*   **`POST /recommend`**: The main endpoint. It asks `ABTestService` which engine to use, then calls `engine.recommend()`.
*   **`POST /admin/models/reload`**: The "Trigger". Tells the system to check the Registry and hot-swap models if a new one is available.

### `src/recommender/engines/hybrid.py`
**Role:** The Logic Core.
*   **`_semantic_search`**: Calls Qdrant. **Crucial Fix:** We essentially patched this to ensure it returns the `payload` (metadata), otherwise, pure semantic matches were lost.
*   **`_keyword_search`**: Calls MongoDB. **Optimization:** Uses `{"$text": ...}` instead of Regex. This uses the specialized Text Index we created, making search `O(log N)` (fast) instead of `O(N)` (slow full scan).
*   **`_reciprocal_rank_fusion`**: The math. It iterates through both lists and sums their reciprocal ranks.

### `src/recommender/services/registry_service.py`
**Role:** The Librarian.
*   **`register_model`**: Called by the Trainer. Saves metadata (`path`, `metrics`) to MongoDB with `status="candidate"`.
*   **`promote_model`**: Atomic operation. Sets all other models of that type to `archived` and the target model to `active`.
*   **`get_active_model`**: Used by the API to find out *what* to load.

### `src/recommender/services/embedding_service.py`
**Role:** The Heavy Lifter.
*   **`load_active_model`**: The smart loader. It checks the registry. If the model on disk matches what's already in memory, it does nothing (fast). If different, it loads the new one.
*   **`embed_text`**: Turns user queries into `[0.1, -0.5, ...]` vectors using the loaded Torch model.

### `src/recommender/database.py`
**Role:** The Connection Manager.
*   **`_ensure_collections`**: **Critical.** This is where we define the indices. We added `("name", "text")` here. Without this, the keyword search would crash the server on a 4.2M dataset.
*   **Refactor Note:** This file was recently updated to use `src.db.config`, ensuring it shares connection strings with the rest of the app (DRY Principle).

---

## 5. Data Flow Example: A "Hot Swap"

1.  **Training:** The training container finishes fine-tuning a model. It saves weights to `/app/models/embedding/v2_timestamp/`.
2.  **Registration:** The trainer inserts `{ "model_id": "v2", "path": "embedding/v2...", "status": "candidate" }` into MongoDB.
3.  **Promotion:** An admin (or script) calls `promote_model("v2")`. MongoDB updates "v2" to `active` and "v1" to `archived`.
4.  **Reload:** The admin calls `POST /admin/models/reload`.
5.  **Switch:**
    *   `EmbeddingService` queries MongoDB -> sees "v2" is active.
    *   It compares "v2" with currently loaded "v1".
    *   It loads "v2" from disk into a temp variable.
    *   It swaps `self.model = new_model`.
    *   Garbage collection frees "v1".
6.  **Result:** Users instantly start getting better recommendations without any downtime.

---

## 6. Future Improvements for You to Build

1.  **Online Learning:** Instead of batch training, update the user preference vectors in Real-Time as they click.
2.  **Explainability:** Use an LLM to generate a natural language string explaining *why* a repo was picked (e.g., "Because you liked React, and this is a fast React alternative").
3.  **Visualizations:** Add a Grafana dashboard to track the `EvaluationMetrics` (NDCG, CTR) stored in MongoDB.

---
**Prepared for:** Aspiring Software Engineer / Git-Query Maintainer
![[Git-Query_System_Report 1]]