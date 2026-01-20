**Tags:** #concept #nlp #preprocessing **Related:** [[Lemmatization]], [[Tokenization]]

## Definition
A crude heuristic process that chops off the ends of words (suffixes) to reduce them to their base form (stem).

## Characteristics
- **Mechanism:** Uses rule-based string manipulation (e.g., "if word ends in 'ing', remove 'ing'").
    
- **Output:** The resulting stem is **not** always a valid word in the dictionary.
    - _Example:_ "Running" $\rightarrow$ "Run"
    - _Example:_ "Berries" $\rightarrow$ "Berri" (Porter Stemmer behavior)
        
- **Goal:** To reduce dimensionality by grouping variants of a word.