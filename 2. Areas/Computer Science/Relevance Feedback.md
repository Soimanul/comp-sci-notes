**Tags:** #concept #nlp
**Related:** [[Information Retrieval]]

## Definition
Relevance feedback is a process in information retrieval where the system refines the results based on user interaction. Documents marked as relevant are used to reinforce certain terms, while non-relevant documents reduce their influence.

## Core Mechanics
Relevance is not static; it is an adaptive, comparative notion. A common method for updating the query vector is the **Rocchio-style update equation**:

$$ \vec{q}_{i+1} = \vec{q}_i + \frac{\beta}{R} \sum_{j=1}^{R} \vec{r}_j - \frac{\gamma}{S} \sum_{l=1}^{S} \vec{s}_l $$

Where:
- $\vec{q}_i$ is the original query.
- $\vec{r}_j$ are vectors of relevant documents (R total).
- $\vec{s}_l$ are vectors of non-relevant documents (S total).
- $\beta$ and $\gamma$ are weights controlling how far the query is pushed toward or away from these sets.

## Significance
Relevance feedback allows the query to "evolve" to better represent the user's information need, even if that need was vaguely specified in the original query.
