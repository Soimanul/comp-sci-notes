**Tags:** #hub #reco #dl
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> The Wide & Deep model (Google, 2016) jointly trains a wide linear component for memorisation (learning specific feature co-occurrences from history) and a deep neural network for generalisation (discovering latent patterns from embeddings). It is the canonical architecture for app recommendation in production at Google Play.

## Overview

Production recommendation requires both memorising known associations (e.g. "users who install game X also install game Y") and generalising to unseen combinations. Wide & Deep solves this with a single jointly trained model.

## Knowledge Map

- [[Wide and Deep Model]]
- [[Memorization vs Generalization in Reco]]

> [!question]- Exam Questions
> - What is the difference between memorisation and generalisation in the Wide & Deep context?
> - What does the wide component contribute that the deep component cannot?
> - What features go into the wide component vs. the deep component?
> - How are the wide and deep outputs combined at the final layer?
> - What is the deployment context of Wide & Deep (which application was it designed for)?
