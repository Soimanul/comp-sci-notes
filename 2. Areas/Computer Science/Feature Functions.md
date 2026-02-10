**Tags:** #concept #nlp
**Related:** [[Maximum Entropy Classifier]], [[Logistic Regression]]

## Definition
Feature functions $f_i(x, y)$ are real-valued functions that encode specific properties or associations between the input $x$ and the label $y$ that the model should respect.

## Core Mechanics
In text classification, a feature function often checks for the presence of a specific word in a document with a specific label:

$$ f_i(x, y) = \begin{cases} 1 & 	ext{if word "spam" exists in document } x 	ext{ and } y = 	ext{"Spam"} \ 0 & 	ext{otherwise} \end{cases} $$

During training, the model learns a weight $\lambda_i$ for each feature function. These weights represent the strength of the association.

## Significance
Feature functions allow for the integration of diverse types of knowledge into the classifier. Unlike Naïve Bayes, which treats words as independent, MaxEnt models can handle overlapping or redundant features more gracefully by adjusting the weights $\lambda_i$.
