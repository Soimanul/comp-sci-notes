**Tags:** #concept #nlp
**Related:** [[Evaluation Metrics for Classifiers]]

## Definition
A confusion matrix is a table used to describe the performance of a classification model on a set of test data for which the true values are known.

## Structure
For a binary classifier, the matrix is a $2 	imes 2$ grid:

| | Predicted: Negative | Predicted: Positive |
| :--- | :--- | :--- |
| **True: Negative** | True Negative (TN) | False Positive (FP) |
| **True: Positive** | False Negative (FN) | True Positive (TP) |

### Errors
- **Type I Error (False Positive)**: Predicting a positive result when it is negative (False Alarm).
- **Type II Error (False Negative)**: Predicting a negative result when it is positive (Miss).

## Significance
The confusion matrix provides a granular view of where the model is failing, allowing developers to calculate all core evaluation metrics and understand the practical consequences of different error types.
