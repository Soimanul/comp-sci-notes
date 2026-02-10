**Tags:** #concept #nlp
**Related:** [[Information Retrieval]], [[TF–IDF]], [[Cross-Entropy Loss]]

## Definition
Statistical relevance is a measure of how well a document (or word) distinguishes itself in a given context based on frequency and distribution, rather than semantic understanding.

## Core Mechanics
Statistical relevance models operate on the principle of **surprise**. 
- Informative events are those that are statistically unexpected.
- Words that appear in almost every document carry little information.
- Rare words are assigned high probability/weight because they help discriminate between documents.

This intuition is closely related to **Cross-Entropy**, which measures how unexpected observed data are under a given probabilistic model.

### From Document to Word Relevance
The same logic used for ranking documents can be applied at the level of words. By treating a context as a "bag of words," one can predict the next word by choosing the one that minimizes expected surprise (maximizing statistical association).

## Significance
Statistical relevance allows for fluent-looking text generation (like ELIZA or basic N-grams) and effective search without needing to model syntax or intention. However, it is limited by its lack of true semantic understanding.
