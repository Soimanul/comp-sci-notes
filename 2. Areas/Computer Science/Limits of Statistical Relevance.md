>[!tip]
>**Tags:** #concept #nlp
**Related:** [[Statistical Relevance]], [[Information Retrieval]]

## Definition
Statistical relevance models, while effective for retrieval and basic generation, have fundamental limitations because they operate entirely on surface-level patterns of usage.

## Core Limitations
1. **No Word Order**: Models like Bag-of-Words ignore the sequence of characters/words.
2. **No Compositional Meaning**: They cannot capture how the meaning of a sentence is built from its parts (e.g., "The dog bit the man" vs "The man bit the dog").
3. **No Paraphrase Equivalence**: They may fail to recognize that two differently worded sentences express the same intent.
4. **No World Knowledge**: They lack a grounding in reality or external facts beyond the corpus.

## Significance
These limitations motivate the development of more expressive models, such as those incorporating syntax or deep neural representations, which can move beyond "relevance without understanding."
