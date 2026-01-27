**Tags:** #concept #nlp #preprocessing 
**Related:** [[Stemming]], [[Morphemes]], [[Subwords]]

## Definition
The process of reducing a word to its base dictionary form, known as the **Lemma**. Unlike stemming, it considers the context and part of speech.

## Characteristics
- **Mechanism:** Uses a vocabulary and morphological analysis.

- **Output:** Always a valid dictionary word.
    - _Example:_ "Better" $\rightarrow$ "Good" (Stemming would fail here).
    - _Example:_ "Meeting" (noun) $\rightarrow$ "Meeting" vs "Meeting" (verb) $\rightarrow$ "Meet".

- **Cost:** Computationally more expensive than stemming.