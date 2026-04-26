**Tags:** #hub #reco
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> The inner product in Matrix Factorization cannot capture all interaction patterns. Factorization Machines (FM) generalise MF by modelling all pairwise feature interactions using latent factor dot products, enabling them to work on any feature set. Field-Aware Factorization Machines (FFM) extend FM by learning separate embeddings per feature field.

## Overview

This session motivates why plain MF is limited, then introduces Factorization Machines as a unified framework that subsumes MF, logistic regression, and polynomial regression — all while remaining efficient enough for production.

## Knowledge Map

- [[Inner Product Limitation]]
- [[Factorization Machines]]
- [[Field-Aware Factorization Machines]]

> [!question]- Exam Questions
> - Why does the inner product fail in Matrix Factorization when the ranking cannot be expressed as a dot product in low-dimensional space?
> - Write the FM model equation for degree-2 interactions and explain each term.
> - How does FM reduce to matrix factorization as a special case?
> - What is the computational trick that reduces FM interaction computation from O(kn²) to O(kn)?
> - What is the difference between FM and FFM? When would you prefer FFM?
