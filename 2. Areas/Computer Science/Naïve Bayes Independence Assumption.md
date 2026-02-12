**Tags:** #concept #nlp
**Related:** [[Naïve Bayes]], [[2. Areas/Computer Science/Bayes' Theorem]]

## Definition
The "Naïve" part of Naïve Bayes comes from the strong assumption that all features (words) in a document are **conditionally independent** of each other given the class.

## Core Mechanics
Mathematically, this simplifies the likelihood calculation:

$$ P(w_1, w_2, ..., w_n | Class) \approx \prod_{i=1}^{n} P(w_i | Class) $$

Instead of needing to know the joint probability of every combination of words (which is computationally impossible for large vocabularies), we only need to know the probability of each individual word appearing in a given class.

## Significance
This assumption is technically false in natural language (words depend on context and syntax), but it greatly simplifies the model and often works surprisingly well for text classification tasks like spam detection.
