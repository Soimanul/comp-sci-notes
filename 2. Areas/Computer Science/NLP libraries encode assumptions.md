**Tags:** #concept #nlp #python #libraries #pipelines  
**Related:** [[NLP Libraries and Pipelines]] · [[Library tradeoffs - control vs robustness]] · [[Common NLP pipeline stages]]

## Definition
An NLP library is not just a toolbox of functions; it encodes a set of assumptions about language processing through its default representations, pipeline structure, and what it exposes as “the normal workflow”.

## What a library implicitly decides
- What the basic units are (tokens, sentences, spans, documents).
- Which steps are standard (normalization, tokenization, tagging, parsing, NER, etc.).
- Which representations are primary (rule-based structures vs statistical models vs pretrained embeddings).
- How much control the user gets versus what is hidden behind defaults.

## Why this matters
Choosing a library is also choosing a set of modeling and engineering tradeoffs, which shapes what kinds of NLP solutions are easy, reliable, or even feasible within that ecosystem.
