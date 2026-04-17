**Tags:** #concept #nlp #pos
**Related:** [[POS Tagging]], [[Penn Treebank POS Tagset]]

## Definition

Universal POS (UPOS) tags are a cross-linguistically valid, coarse-grained tagset of 17 categories defined by the Universal Dependencies (UD) project. They enable direct comparison and transfer of NLP models across languages.

> [!info] Key Intuition
> UPOS deliberately sacrifices English-specific detail for cross-lingual portability — 17 categories that map cleanly onto the grammatical structures of most human languages.

## Core Mechanics

The 17 UPOS categories:
`NOUN`, `VERB`, `ADJ`, `ADV`, `PRON`, `DET`, `ADP`, `AUX`, `CCONJ`, `SCONJ`, `PART`, `NUM`, `PUNCT`, `SYM`, `INTJ`, `PROPN`, `X` (other)

Mapping from PTB: NN/NNS/NNP/NNPS → `NOUN` or `PROPN`; VB/VBD/VBG/VBN/VBP/VBZ → `VERB` or `AUX`; JJ/JJR/JJS → `ADJ`.

UPOS is used in all Universal Dependencies treebanks (100+ languages) and is the standard tagset for multilingual POS benchmarks.

> [!warning] Common Misconception
> UPOS is not simply "simplified PTB." Some UPOS categories (`AUX`, `CCONJ`, `SCONJ`) have no direct PTB equivalent and require language-specific disambiguation rules to assign correctly.
