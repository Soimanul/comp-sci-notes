**Tags:** #concept #nlp
**Related:** [[Regular Expressions (Regex)]], [[Regex Basic Patterns]]

## Definition
Greedy behavior refers to the default tendency of regular expression quantifiers (`*`, `+`, `{n,m}`) to match as much text as possible.

## Core Mechanics
By default, quantifiers will expand to the largest possible match that still allows the rest of the expression to succeed.

### The Problem
If matching text between quotes:
`".*"` in `"Hello" and "World"` will match `"Hello" and "World"` instead of just `"Hello"`.

### The Solution: Lazy Matching
Appending a `?` to a quantifier makes it **lazy** (or non-greedy), meaning it will match as little text as possible.
`".*?"` in `"Hello" and "World"` will match `"Hello"` and `"World"` as two separate matches.

## Significance
Understanding greedy behavior is crucial for preventing unexpected results when delimiters (like quotes, tags, or brackets) repeat or when multiple matches are possible in a single string.
