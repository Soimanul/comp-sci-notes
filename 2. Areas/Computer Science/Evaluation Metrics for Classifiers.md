**Tags:** #concept #nlp
**Related:** [[Text Classification]], [[Confusion Matrix]]

## Definition
Evaluation metrics are quantitative measures used to assess the performance of a classification model. Relying on a single metric (like accuracy) can be misleading, especially with imbalanced datasets.

## Core Metrics
All evaluation metrics are derived from the **Confusion Matrix** (True Positives, False Positives, True Negatives, False Negatives).

| Metric | Formula | Description |
| :--- | :--- | :--- |
| **Accuracy** | $\frac{TP + TN}{Total}$ | Proportion of correct predictions. |
| **Precision** | $\frac{TP}{TP + FP}$ | Reliability of positive predictions ("Of all flagged as spam, how many were actually spam?"). |
| **Recall** | $\frac{TP}{TP + FN}$ | Ability to find all positive instances ("Of all spam, how many did we find?"). |
| **Specificity** | $\frac{TN}{TN + FP}$ | Ability to detect negatives. |
| **NPV** | $\frac{TN}{TN + FN}$ | Reliability of negative predictions. |

## Baseline Models
To determine if a model is learning anything useful, its performance is compared against simple baselines:

- **Random Classifier**: Labels observations randomly based on uniform probability (usually ~50% metrics for binary classification).

- **Prevalence Classifier**: Always predicts the most common label in the dataset. While it may achieve high accuracy on imbalanced datasets, it fails on precision, recall, and specificity for the minority class.

## Significance
Different tasks prioritize different metrics. In medical diagnosis, high **Recall** is critical to avoid missing cases. In spam filtering, high **Precision** is preferred to avoid blocking important emails.
