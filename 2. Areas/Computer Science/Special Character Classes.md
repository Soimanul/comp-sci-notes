**Tags:** #concept #nlp
**Related:** [[Regular Expressions (Regex)]], [[Regex Basic Patterns]]

## Definition
Special character classes are shorthand notations in regular expressions that represent common sets of characters (digits, words, whitespace) or specific positions in a string (anchors).

## Core Mechanics
| Operator | Behavior | Example |
| :--- | :--- | :--- |
| `\d` | Any digit [0-9] | `\d{3}` matches `123` |
| `\D` | Any non-digit | `\D` matches `a`, ` ` |
| `\w` | Word character [a-zA-Z0-9_] | `\w+` matches `word_123` |
| `\W` | Non-word character | `\W` matches `!`, `?` |
| `\s` | Whitespace (space, tab, newline) | `\s` matches ` ` |
| `\S` | Non-whitespace | `\S` matches `x` |
| `
` | Newline character | |
| `	` | Tab character | |
| `\b` | Word boundary | `\bcat\b` matches `cat` but not `catapult` |

## Significance
These classes make regular expressions more concise and readable, allowing developers to define complex character sets with a single escape sequence. Understanding the difference between character matches and positional matches (like boundaries) is essential for writing predictable patterns.
