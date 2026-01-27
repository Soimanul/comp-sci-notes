**Tags:** #concept #nlp #preprocessing 
**Related:** [[Morphemes]], [[Subwords]], [[N-gram Model]]

## Definition
The process of breaking a stream of text into smaller, meaningful units called **tokens**. These tokens can be words, characters, or subwords.

## Levels of Tokenization
1. **Word-Level:** Splitting by spaces or punctuation.
    - _Issue:_ Large vocabulary size; treats "cat" and "cats" as unrelated.

2. **Character-Level:** Splitting into individual characters.
    - _Issue:_ Loss of semantic meaning; sequences become very long.

3. **Subword-Level:** Splitting into frequent morphological units (e.g., "un-friend-li-ness").
    - _Advantage:_ Balances vocabulary size and semantic meaning.