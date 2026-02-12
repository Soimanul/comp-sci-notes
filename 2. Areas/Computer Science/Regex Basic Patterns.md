**Tags:** #concept #nlp
**Related:** [[Regular Expressions (Regex)]], [[Formal Language Theory]]

## Definition
Basic patterns in regular expressions are the fundamental operators used to construct search **strings**. They include literal characters, wildcards, anchors, and quantifiers.

## Core Mechanics
| <center>Operator</center> | <center>Behavior</center>                     | <center>Example</center>                                    |
| :------------------------ | :-------------------------------------------- | :---------------------------------------------------------- |
| `.`<center></center>      | Wildcard, matches any character               | `c.t` matches `cat`, `cut`                                  |
| `^`                       | Matches start of string                       | `^abc` matches `abc123` at the start but not `xabc123`      |
| `$`                       | Matches end of string                         | `abc$` matches `123abc` at the end but not `123abcc`        |
| `[abc]`                   | Matches any of the set                        | `[abc]` matches `a`, `b`, or `c`                            |
| `[A-Z0-9]`                | Matches any range                             | `[A-Z0-0]` matches any uppercase letter and number from 0-9 |
| `ed\|ing\|s`              | Disjunction (OR)                              | `ed\|ing\|s` matches `ed`, `ing` or `s`                     |
| `*`                       | Zero or more of prev item (Kleene Closure)    | `ab*` matches `a`, `ab`, `abbb`                             |
| `+`                       | One or more of prev item                      | `ab+` matches `ab`, `abbb`                                  |
| `?`                       | Zero or one                                   | `colou?r` matches `color` and `colour`                      |
| `{n}`                     | Exactly n repeats                             | `\d{4}` matches `2025`                                      |
| `{n,}`                    | At least n repeats                            | `a{2,}` matches `aa`, `aaa`, `aaaa`                         |
| `{,n}`                    | No more than n repeats                        | `a{,3}` matches `a`, `aa`, `aaa`                            |
| `{m, n}`                  | At least m repeats and no more than n repeats | `a{2, 4}` matches `aa`, `aaa`, `aaaa`                       |
| `a(b\|c)+`                | Groups / Scope                                | `(add\|ing\|s)+` matches `addings`,`sing`, or `adding`      |

## Significance
These operators allow for the definition of infinite sets of strings using a finite, algebraic notation. They are the building blocks for all complex pattern matching tasks in text processing.
