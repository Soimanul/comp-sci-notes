**Tags:** #concept #nlp #pos
**Related:** [[POS Tagging]], [[Universal POS Tags]]

## Definition

The Penn Treebank (PTB) POS tagset is a 45-tag annotation scheme developed for the Wall Street Journal corpus. It is the standard tagset for English NLP benchmarks and the basis for most English POS tagging evaluations.

> [!info] Key Intuition
> PTB tags are fine-grained English-specific: they distinguish singular/plural nouns (NN/NNS), base/comparative/superlative adjectives (JJ/JJR/JJS), and five verb forms — detail that universal tagsets deliberately collapse for cross-lingual portability.

## Core Mechanics

Key tag groups:
| Tags | Category |
|---|---|
| NN, NNS, NNP, NNPS | Nouns (common sg, common pl, proper sg, proper pl) |
| VB, VBD, VBG, VBN, VBP, VBZ | Verbs (base, past, gerund, past-part, non-3sg present, 3sg present) |
| JJ, JJR, JJS | Adjectives (base, comparative, superlative) |
| RB, RBR, RBS | Adverbs |
| DT | Determiner |
| IN | Preposition or subordinating conjunction |
| CC | Coordinating conjunction |
| PRP, PRP$ | Personal pronoun, possessive pronoun |
| WDT, WP, WP$, WRB | Wh-words |

Special tags: `.` `,` `:` for punctuation; `$` for currency; `#` for hash.

> [!example]- Worked Example
> "The quick brown fox jumps over the lazy dog."
> DT JJ JJ NN VBZ IN DT JJ NN .

## Significance

PTB tags remain the benchmark standard for English despite their English-centric design. Cross-lingual work typically maps to Universal POS tags instead.
