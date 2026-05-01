**Tags:** #topic #hub #nlp
**Related:** [[Natural Language Processing]], [[Deep Learning Architectures]]

## Overview
This hub bridges classical NLP pipelines (Bag-of-Words, TF–IDF, statistical classifiers) and the neural framework, where the model itself learns input representations jointly with the prediction task. It covers the building blocks of feedforward neural networks, how parameters are learned through gradient-based optimization, and how words — discrete symbols — are mapped to dense vectors that a neural model can consume.

> [!abstract]- TL;DR
> Feedforward neural networks compose parameterized linear layers with nonlinear activations to learn task-specific representations. For NLP they sit on top of an embedding lookup that maps words to dense vectors, and parameters are trained end-to-end by minimizing a loss with backpropagation.

## Knowledge Map

### 1. Building Blocks
- [[Single Neuron Computation]]
- [[Layer Vector Computation]]
- [[Feedforward Neural Network]]
- [[Activation Functions]]

### 2. Training
- [[Backpropagation]]
- [[Epoch]]
- [[Stochastic Gradient Descent (SGD)]]
- [[Neural Network Loss Functions]]
- [[Neural Network Optimizers]]

### 3. From Words to Vectors
- [[One-Hot Encoding]]
- [[Embedding Matrix]]
- [[Word Embeddings]]

### 4. Neural Text Classification
- [[Sentence Average Embedding]]

> [!question]- Common Exam Questions
> - Why are nonlinear activation functions essential in a multi-layer network?
> - How does the embedding matrix relate to the one-hot encoding of a word?
> - What changes when moving from Batch GD to SGD to Mini-Batch GD?
> - Given a sentence, describe a minimal neural pipeline that classifies it.
