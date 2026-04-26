**Tags:** #hub #reco #dl
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> Sequential recommendation models the order of a user's interactions to predict the next item, while session-based recommendation operates on anonymous short interaction sequences without user history. GRU4Rec (recurrent), Caser (CNN with dilated convolutions), and SASRec (Transformer) are the key architectures for capturing sequential dynamics.

## Overview

User preferences are not static — the last item a user interacted with is often the best predictor of the next. This session covers the progression from RNN-based to CNN-based to Transformer-based sequential recommendation.

## Knowledge Map

- [[Sequential vs Session-Based Recommendation]]
- [[GRU for Recommendations]]
- [[LSTM for Recommendations]]
- [[CNN for Sequential Recommendations]]
- [[Dilated Convolutions for Recommendations]]
- [[Transformer for Sequential Recommendations]]

> [!question]- Exam Questions
> - What is the difference between sequential recommendation and session-based recommendation?
> - Why is GRU preferred over LSTM in GRU4Rec?
> - How does a CNN capture sequential patterns in a user's interaction history?
> - What is the role of dilated convolutions in capturing long-range dependencies?
> - How does the Transformer (SASRec) handle the sequential recommendation task? What masking is applied?
