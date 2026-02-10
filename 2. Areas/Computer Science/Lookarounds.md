**Tags:** #concept #nlp
**Related:** [[Regular Expressions (Regex)]], [[Regex Basic Patterns]]

## Definition
Lookarounds are non-consuming regular expression constructs that test the immediate context of a pattern without actually including those characters in the match.

## Core Mechanics
Lookarounds allow for enforcing constraints on what must or must not appear before or after a match.

| Name | Syntax | Behavior |
| :--- | :--- | :--- |
| Positive Lookahead | `(?=...)` | Matches if followed by `...` |
| Negative Lookahead | `(?!...)` | Matches if NOT followed by `...` |
| Positive Lookbehind | `(?<=...)` | Matches if preceded by `...` |
| Negative Lookbehind | `(?<!...)` | Matches if NOT preceded by `...` |

### Example
To match a number only if it is followed by a percentage sign, but without including the `%` in the match:
`\d+(?=%)` matches `5` in `51%`.

## Significance
Lookarounds are essential for precise extraction in NLP preprocessing, especially when the surrounding text provides necessary context but should not be part of the extracted token (e.g., currency symbols, units).
