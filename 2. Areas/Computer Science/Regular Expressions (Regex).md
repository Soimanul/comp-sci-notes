**Tags:** #topic #hub #nlp
**Related:** [[Natural Language Processing]], [[NLP Preprocessing]]

## Overview
Regular expressions (regex) are a formal language for specifying patterns in text. In the context of NLP, they serve as a tool for transforming unstructured **raw text** into **structured data** that can be counted, compared, and eventually classified.

Formally, a regular expression can be understood as an algebraic notation for characterizing a set of strings.

> [!example] 
> For example, the following regular expression describes a broad class of URLs:
> ```
> \b(?:(?:https?|ftp):\/\/)?(?:www\.)?[a-zA-Z0-9-]+(?:\.[a-zA-Z]{2,}(?:\/[^\s#]*)?(?:\?[^\s#]*)?(?:#[^\s]*)?\b
> ```
## Knowledge Map
### 1. Fundamentals
- [[Regex Basic Patterns]]
- [[Special Character Classes]]

### 2. Advanced Pattern Matching
- [[Lookarounds]]
- [[Greedy vs Lazy Matching]]

### 3. Application
- [[Regex in NLP Pipeline]]
