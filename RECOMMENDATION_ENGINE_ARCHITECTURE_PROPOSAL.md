## Executive Summary
This document outlines a robust, modern, and high-level architecture for the Git-Query recommendation engine. The system is designed to provide personalized repository recommendations by leveraging multi-stage retrieval, real-time feedback loops, and automated MLOps pipelines. It transitions the project from simple vector search to a production-grade machine learning serving stack.

## 1. System Overview
The architecture is divided into two primary paths: the Hot Path (Real-time Inference) and the Cold Path (Asynchronous Training and Processing). This separation ensures low-latency responses for users while maintaining high-quality model updates.

### Core Components:
- **API Gateway**: Orchestrates requests and manages user sessions.
- **Recommender API**: Handles inference, filtering, and final ranking.
- **Qdrant Vector Database**: Stores repository and user embeddings for fast retrieval.
- **MongoDB**: Serves as the primary data store for raw repository metadata and interaction history.
- **Redis**: Manages session data and serves as the message broker for asynchronous tasks.
- **Celery Workers**: Handle embedding generation and ETL processes.

## 2. Multi-Stage Retrieval and Ranking Pipeline
To balance performance and accuracy, the system employs a three-stage pipeline:

### Stage 1: Candidate Generation (Retrieval)
- **Objective**: Reduce the search space from millions of repositories to the top 100-200 candidates.
- **Method**: Vector similarity search in Qdrant using dense embeddings.
- **Filters**: Pre-filtering based on hard constraints such as programming language, minimum star count, and license type.

### Stage 2: Scoring (Ranking)
- **Objective**: Re-rank candidates using a more computationally expensive but accurate model.
- **Method**: A lightweight ranking model (e.g., XGBoost, LightGBM, or a Cross-Encoder) that incorporates user-specific features and interaction history.
- **Input**: User profile features, repository metadata, and initial similarity scores.

### Stage 3: Post-Processing and Diversity
- **Objective**: Ensure the final results are diverse and relevant to the current session.
- **Method**: Deduplication, business logic application (e.g., excluding repositories already in the user's library), and diversity re-ranking to avoid "filter bubbles."

## 3. Inference Stack (Hot Path)
The inference stack is built for high throughput and low latency.

- **Stateless Scaling**: The Recommender API is containerized and can be horizontally scaled based on request volume.
- **In-Memory Caching**: Frequently accessed user profiles and recent recommendations are cached in Redis to minimize database lookups.
- **Sidecar Pattern**: Heavy model scoring can be offloaded to dedicated inference sidecars or optimized using runtimes like ONNX.

## 4. Training and MLOps Pipeline (Cold Path)
The system automates the lifecycle of the recommendation models to ensure they stay relevant as data evolves.

- **ETL Pipelines**: Celery tasks extract interaction logs from MongoDB and prepare training datasets.
- **Automated Retraining**: Scheduled jobs trigger model retraining when performance metrics (like Click-Through Rate) drop below a defined threshold or after a set time interval.
- **Model Registry**: Versioned models are stored in a dedicated artifact registry, allowing for safe rollbacks and A/B testing.
- **Validation**: Every new model must pass a battery of offline evaluation tests (e.g., Precision@K, Recall@K, MRR) before being promoted to production.

## 5. Data Flow and Feedback Loop
The "Flywheel" effect is achieved by capturing user interactions to inform future recommendations.

1. **Interaction Capture**: The API Gateway logs clicks, views, and searches.
2. **Real-time Updates**: Interactions trigger background tasks to update the User Interest Vector in Qdrant.
3. **Feature Enrichment**: These interactions are periodically aggregated into the MongoDB data store to be used in the next training cycle.

## 6. Scaling and Reliability
- **Health Monitoring**: Prometheus and Grafana are used to monitor API latency, model drift, and system health.
- **Resilience**: Circuit breakers protect the Gateway from slow responses in the Recommender API.
- **Cold Start Mitigation**: New repositories are automatically vectorized and indexed as part of the ingestion pipeline, ensuring they are available for recommendation immediately.

## 7. Technical Recommendations
- **Embeddings**: Utilize modern transformers (e.g., BGE-Small or specialized Code-BERT models) for representing repository content.
- **Database**: Qdrant for vector operations due to its robust filtering support.
- **Orchestration**: Docker Compose for local/dev environments, transitioning to Kubernetes for production scaling.
- **Monitoring**: Focus on Mean Reciprocal Rank (MRR) as a primary metric for recommendation success.
