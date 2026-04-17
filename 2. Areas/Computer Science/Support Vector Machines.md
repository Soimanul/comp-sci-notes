**Tags:** #hub #nlp #ml #svm
**Related:** [[Natural Language Processing]], [[Logistic Regression]], [[Naïve Bayes]]

## Overview

Support Vector Machines (SVMs) are supervised learning models that find the maximum-margin hyperplane separating two classes. Their geometric formulation, dual representation, and kernel trick make them especially powerful for high-dimensional text classification tasks.

> [!abstract]- TL;DR
> An SVM finds the decision boundary with the largest margin between classes, controlled by support vectors alone. The kernel trick lets SVMs operate in high-dimensional (even infinite-dimensional) feature spaces without ever computing those coordinates explicitly.

## Knowledge Map

### 1. Core Geometry
- [[Maximum Margin Classifier]]
- [[Support Vectors]]

### 2. Handling Non-Separable Data
- [[Soft Margin SVM]]
- [[Slack Variables]]

### 3. Non-Linear Extension
- [[Kernel Trick]]
- [[Kernel Functions]]

### 4. Optimization
- [[SVM Dual Formulation]]

> [!question]- Common Exam Questions
> - What are support vectors and why does only they determine the decision boundary?
> - Explain the role of the regularisation parameter $C$ in soft-margin SVMs.
> - How does the kernel trick allow SVMs to classify non-linearly separable data?
> - Write the SVM primal optimisation objective and describe each term.
