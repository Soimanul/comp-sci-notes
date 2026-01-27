**Tags:** #concept #nlp #pipelines  
**Related:** [[NLP Libraries and Pipelines]] · [[NLP libraries encode assumptions]] · [[spaCy]] · [[NLTK]]

## Definition
Common NLP pipeline stages are the typical processing steps that transform raw text into structured outputs, where different libraries differ mainly in how explicit, configurable, or automated these stages are.

## Typical stages
- **Text normalization:** casing, unicode cleanup, punctuation handling.
- **Tokenization:** splitting text into tokens (and often sentences).
- **Linguistic annotation:** POS tagging, lemmatization, morphological features.
- **Syntactic analysis:** dependency parsing or constituency parsing.
- **Semantic-ish extraction:** named entity recognition, phrase chunks, simple relations.
- **Vectorization:** sparse features (BoW/TF–IDF) or dense embeddings.
- **Task layer:** classification, similarity, retrieval, question answering, etc.

## Pipeline implication
A “pipeline” is not only a sequence of functions; it defines intermediate representations and constrains how downstream tasks consume upstream outputs.
