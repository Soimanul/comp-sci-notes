**Tags:** #concept #nlp
**Related:** [[Regular Expressions (Regex)]], [[Formal Language Theory]]

## Definition
Basic patterns in regular expressions are the fundamental operators used to construct search strings. They include literal characters, wildcards, anchors, and quantifiers.

## Core Mechanics
| Operator | Behavior | Example |
| :--- | :--- | :--- |
| `.` | Wildcard, matches any character | `c.t` matches `cat`, `cut` |
| `^` | Matches start of string | `^abc` matches `abc` at the start |
| `$` | Matches end of string | `abc$` matches `abc` at the end |
| `[abc]` | Matches any of the set | `[abc]` matches `a`, `b`, or `c` |
| `[a-z]` | Matches a range | `[a-z]` matches any lowercase letter |
| `\|` | Disjunction (OR) | `ed|ing` matches `ed` or `ing` |
| `*` | Zero or more (Kleene Closure) | `ab*` matches `a`, `ab`, `abbb` |
| `+` | One or more | `ab+` matches `ab`, `abbb` |
| `?` | Zero or one | `color?s` matches `colors` and `colour` |
| `{n}` | Exactly n repeats | `\d{4}` matches `2025` |
| `()` | Groups / Scope | `(add\|ing)` matches `add` or `ing` |

## Significance
These operators allow for the definition of infinite sets of strings using a finite, algebraic notation. They are the building blocks for all complex pattern matching tasks in text processing.
