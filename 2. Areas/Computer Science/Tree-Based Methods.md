**Tags:** #hub #reco
**Course:** [[Chatbots and Recommendation Engines]]
**Semester:** Y3S2

---

> [!abstract]- TL;DR
> Tree-based methods are powerful non-linear models for recommendation tasks involving rich feature sets (e.g. CTR prediction). Decision Trees split on the most informative feature (Gini/Entropy). Random Forests reduce variance via bagging. Gradient Boosting (GBDT, LightGBM, XGBoost) reduces bias iteratively by fitting residuals, and is the dominant method in tabular CTR prediction.

## Overview

When recommendation is framed as a classification or regression problem over structured features (user demographics, item attributes, context), gradient boosted trees are often the best-performing approach. This session covers the tree family from first principles to production-grade implementations.

## Knowledge Map

- [[Decision Trees]]
- [[Gini Index]]
- [[Entropy for Decision Trees]]
- [[Random Forest]]
- [[Gradient Boosting Decision Trees]]
- [[LightGBM]]
- [[XGBoost]]

> [!question]- Exam Questions
> - Explain how a decision tree chooses the best feature and threshold at each split.
> - What is the difference between Gini impurity and information gain (entropy)?
> - How does bagging in Random Forest reduce variance without increasing bias?
> - Describe the gradient boosting process: what does each new tree fit?
> - What are the three key innovations in LightGBM over vanilla GBDT?
> - How does XGBoost regularise the tree structure?
