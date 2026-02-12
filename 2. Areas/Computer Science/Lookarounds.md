**Tags:** #concept #nlp
**Related:** [[Regular Expressions (Regex)]], [[Regex Basic Patterns]]

## Definition
Lookarounds are non-consuming regular expression constructs that test the immediate context of a pattern without actually including those characters in the match.

## Core Mechanics
Lookarounds allow for enforcing constraints on what must or must not appear before or after a match.

| Name                | Syntax     | Behavior                                                                                                   | Examples                                         |
| :------------------ | :--------- | ---------------------------------------------------------------------------------------------------------- | :----------------------------------------------- |
| Positive Lookahead  | `(?=...)`  | Matches a position only if it is followed by the specified pattern                                         | `\d(?=%)` matches `5` in `5%`                    |
| Negative Lookahead  | `(?!...)`  | Matches a position only if it is <font color="#c0504d"><u>not</u></font> followed by the specified pattern | `a(?!n)` matches `a` in `apple` but not in `and` |
| Positive Lookbehind | `(?<=...)` | Matches a position only if it is preceded by the specified pattern                                         | `(?<=\$)\d+` matches `120` in `$120`             |
| Negative Lookbehind | `(?<!...)` | Matches a position only if it is <font color="#c0504d"><u>not</u></font> preceded by the specified pattern | `(?<!-)cat` matches cat but `not` `-cat`         |
## Significance
Lookarounds are essential for precise extraction in NLP preprocessing, especially when the surrounding text provides necessary context but should not be part of the extracted token (e.g., currency symbols, units).
