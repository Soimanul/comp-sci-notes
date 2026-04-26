**Tags:** #hub #reco
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> Learning to Rank (LTR) frames recommendation as an ordering problem rather than rating prediction. Pointwise approaches treat each item independently; pairwise approaches optimise the relative order of pairs; listwise approaches optimise the full ranking directly. Bayesian Personalised Ranking (BPR) is the canonical pairwise method for implicit feedback.

## Overview

Recommendation is fundamentally about producing a ranked list. LTR methods directly optimise ranking objectives, which is more aligned with how end-users experience recommendations than rating RMSE.

## Knowledge Map

- [[Pointwise Loss]]
- [[Pairwise Loss]]
- [[Bayesian Personalized Ranking]]

> [!question]- Exam Questions
> - What is the difference between pointwise, pairwise, and listwise LTR approaches?
> - What implicit assumption does pointwise LTR make that is problematic for recommendations?
> - Write the BPR objective and explain why it is appropriate for implicit feedback data.
> - How does BPR train on (user, positive item, negative item) triples?
> - What is the BPR-MF update rule?
