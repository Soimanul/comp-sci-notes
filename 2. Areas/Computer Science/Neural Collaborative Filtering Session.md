**Tags:** #hub #reco #dl
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> Neural Collaborative Filtering (NCF) replaces the inner product in Matrix Factorization with a neural network, learning richer user-item interactions. The two building blocks are Generalised Matrix Factorization (GMF, a neural reformulation of MF) and an MLP that concatenates embeddings. NeuMF combines both to leverage linear and non-linear interaction patterns simultaneously.

## Overview

This session introduces deep learning for collaborative filtering. The key insight is that the inner product in MF is a limited interaction function — replacing it with a neural network enables the model to learn arbitrary interaction patterns from data.

## Knowledge Map

- [[Neural Collaborative Filtering]]
- [[Generalized Matrix Factorization (GMF)]]
- [[MLP for Neural CF]]

> [!question]- Exam Questions
> - Why is the inner product a limited interaction function for collaborative filtering?
> - How does GMF generalise standard Matrix Factorization?
> - Describe the architecture of the MLP component in NCF.
> - How does NeuMF combine GMF and MLP? What is the fusion layer?
> - What training strategy does NeuMF use to initialise its weights?
