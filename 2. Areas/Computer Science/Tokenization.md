**Tags:** #concept #nlp #preprocessing  
**Related:** [[Morphemes]], [[Subwords]], [[N-gram Model]]

## Definition
Usually the first stage in any Natural Language Processing system. It can be defined as the process of breaking a stream of text into smaller, meaningful units called **tokens**. These tokens can be words, characters, or subwords.

## Levels of Tokenization
1. **Word-Level:** Splitting by spaces or punctuation.
    - _Example tokens (list):_ `["The", "cats", "sleep", "."]`
    - _Issue:_ Large vocabulary size; treats "cat" and "cats" as unrelated.

2. **Character-Level:** Splitting into individual characters.
    - _Example tokens (list):_ `["c", "a", "t", "s"]`
    - _Issue:_ Loss of semantic meaning; sequences become very long.

3. **[[Subwords]]-Level:** Splitting into frequent morphological units. Sometimes they can resemble [[Morphemes]].
    - _Example tokens (list):_ `["un", "friend", "li", "ness"]`
    - _Advantage:_ Balances vocabulary size and semantic meaning.

