[**Tags:** #concept #nlp
**Related:** [[Regular Expressions (Regex)]], [[Regex Basic Patterns]]

## Definition
Special character classes are shorthand notations in regular expressions that represent common sets of characters (digits, words, whitespace) or specific positions in a string (anchors).

## Core Mechanics
| <center>Operator</center> | <center>Behavior</center>        | <center>Example</center>               |
| :------------------------ | :------------------------------- | :------------------------------------- |
| `\d`                      | Any numeric digit [0-9]          | `\d{3}` matches `123`                  |
| `\D`                      | Any character NOT a digit        | `\D` matches `A` or `!`                |
| `\w`                      | Alphanumeric or underscore       | `\w` matches `a`, `1`, or `_`          |
| `\W`                      | Any non-word character           | `\W` matches `&` or `%`                |
| `\s`                      | Any whitespace (space, tab, etc) | `\s` matches ` `                       |
| `\S`                      | Any non-whitespace character     | `\S` matches `x`                       |
| `\n`                      | Newline (Line Feed)              | `\n` matches a line break              |
| `\t`                      | Horizontal Tab                   | `\t` matches a tab indentation         |
| `\r`                      | Carriage Return                  | `\r\n` matches Windows line endings    |
| `\b`                      | Word boundary (position)         | `\bcat\b` avoids matching `catapult`   |
| `\B`                      | Non-word boundary (position)     | `\Babc` matches `aabc` but not `abc`   |
| `\A`                      | Absolute start of string         | `\AHello` matches only at start        |
| `\Z`                      | Absolute end of string           | `Bye\Z` matches only at end            |
| `\\`                      | Literal backslash                | `\\` matches `\`                       |
| `\.`                      | Literal dot                      | `\.` matches `.` (not "any character") |
| `\^`                      | Literal caret                    | `\^` matches `^`                       |
| `\$`                      | Literal dollar sign              | `\$` matches `$`                       |


## Significance
These classes make regular expressions more concise and readable, allowing developers to define complex character sets with a single escape sequence. Understanding the difference between character matches and positional matches (like boundaries) is essential for writing predictable patterns. 
