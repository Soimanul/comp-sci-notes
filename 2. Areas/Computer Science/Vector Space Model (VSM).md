**Tags:** #concept #nlp #vector-space-models #semantic-analysis  
**Related:** [[From Symbols to Spaces]] · [[Bag-of-Words (BoW)]] · [[Term–Document Matrix]] · [[Cosine Similarity]] · [[Distributional Hypothesis]]

## Definition
A **Vector Space Model** represents linguistic objects (documents, queries, words) as **vectors of features** derived from a corpus, placing them in a **continuous numerical space** where **proximity corresponds to similarity**.

## Core Idea: Symbols → Space
- Earlier representations treat language as **discrete symbols** (tokens), where relationships are defined via **order, adjacency, or frequency**.
- In VSMs, **documents and queries become vectors**, and linguistic units are mapped to points in a continuous space.

## Representation
- Each vector dimension corresponds to a **term feature** (typically a vocabulary item).
- The **value of a feature is a term weight**, usually computed as a function of the **term’s frequency in the document** (later refined by weighting schemes like TF–IDF).

## Meaning in VSMs
- Meaning is **not explicitly encoded** as rules.
- Meaning is treated as something that **emerges from relative position** in the vector space (similar things are close).

## What VSM enables
- A unified algebraic framework for comparing:
  - document–document similarity
  - query–document similarity
  - word–word similarity (when words are represented as vectors)

## Limitations / Assumptions (implied by the framework)
- Requires choosing a feature set (vocabulary) and weighting scheme.
- Early VSM instantiations often rely on simplifying assumptions (e.g., BoW-style independence), which motivates later improvements (TF–IDF, LSA, HAL).
