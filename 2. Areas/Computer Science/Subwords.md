**Tags:** #concept #nlp #preprocessing **Related:** [[Tokenization]], [[Morphemes]]

## Definition
Subwords are tokenization units that are smaller than a full word but (often) larger than a single character. They are the standard for modern Deep Learning models (like Transformers).

## [[The OOV Problem]]
Traditional word-level tokenization struggles with **Out-Of-Vocabulary (OOV)** words. If the model hasn't seen the word "unfriendliness" during training, it doesn't know what to do.

## Subword Solution
Subword tokenization breaks unknown words into known chunks based on frequency statistics, rather than strict linguistic rules.

- _Word:_ "unfriendliness"
- _Tokens:_ ["un", "friend", "li", "ness"]

This allows the model to construct the meaning of rare words from frequent components.

## Common Algorithms
- **BPE (Byte-Pair Encoding):** Iteratively merges frequent pairs of characters.
- **WordPiece:** Used in BERT.