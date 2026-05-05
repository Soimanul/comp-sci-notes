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

---

## Self-Test

> [!question] Hard Multiple Choice — 22 Questions

**1.** The pattern `a.*b` applied to *"axxbyybzzb"* with default greedy matching captures:
- A. *"axxb"*
- B. *"axxbyybzzb"* — greedy `.*` extends to the last possible *b*
- C. *"axxbyyb"*
- D. No match

> [!success]- Answer
> **B.** Greedy quantifiers consume as much as possible while still allowing the overall match; the regex backtracks to the last *b*.

**2.** Switching `.*` to `.*?` in the same pattern returns:
- A. The shortest match: *"axxb"*
- B. No match
- C. The same as greedy
- D. *"yyb"*

> [!success]- Answer
> **A.** Lazy/non-greedy quantifiers consume the *minimum* needed for the overall match.

**3.** Which character class matches Unicode word characters in Python's `re` engine *only* if the `re.UNICODE` flag (or default Py3 behavior) is in effect?
- A. `\d`
- B. `\w` — covers letters, digits, underscore, and non-ASCII letters in Py3 default
- C. `\s`
- D. `\b`

> [!success]- Answer
> **B.** `\w` is Unicode-aware in Py3 by default; pre-Py3 you needed the explicit flag.

**4.** A positive *lookahead* `(?=…)`:
- A. Consumes the matched characters
- B. Asserts a condition without consuming characters (zero-width assertion)
- C. Anchors to the start of the string
- D. Disables greedy matching

> [!success]- Answer
> **B.** Lookarounds check; they don't advance the cursor — useful for "matched X *followed by* Y, but only return X."

**5.** `\bcat\b` will *not* match in which of these strings?
- A. *"my cat sleeps"*
- B. *"the catalogue is here"*
- C. *"a cat-like grace"*
- D. *"Cat."* (with case-insensitive flag)

> [!success]- Answer
> **B.** *catalogue* contains *cat* but no word boundary follows; `\b` requires a transition between word and non-word character.

**6.** Why is regex insufficient as the *sole* tokenizer for production NLP?
- A. It is too fast
- B. It cannot handle clitics, contractions, multiword expressions, or language-specific morphology robustly across the long tail
- C. It cannot match digits
- D. It only works on English

> [!success]- Answer
> **B.** Regex is brittle for the full tokenization problem — pragmatic NLP uses regex for narrow extraction tasks, not as the whole tokenizer.

**7.** Catastrophic backtracking arises from:
- A. Using lookbehinds
- B. Nested quantifiers like `(a+)+` on long inputs that don't match — exponential alternative-paths
- C. Non-Unicode characters
- D. Missing flags

> [!success]- Answer
> **B.** Patterns like `(a+)+b` against `"aaaa…"` (no terminal *b*) explore exponentially many partitions before failing.

**8.** A negative lookbehind is denoted:
- A. `(?<=…)`
- B. `(?<!…)`
- C. `(?!…)`
- D. `(?:…)`

> [!success]- Answer
> **B.** `(?<!X)Y` matches *Y* only when *not* preceded by *X*. `(?!…)` is *negative lookahead*.

**9.** Which regex correctly extracts the year from *"on 2024-08-13 we shipped"* assuming dates are `YYYY-MM-DD`?
- A. `\d{4}` (over-matches — would also catch 4-digit non-years)
- B. `\b(\d{4})-\d{2}-\d{2}\b` — anchors with word boundaries and structure
- C. `^\d+$`
- D. `(\d{4})-(\d{2})`

> [!success]- Answer
> **B.** B uses both word boundaries and the date shape to avoid false positives; A is too permissive.

**10.** In NLP preprocessing, regex is most valuable for:
- A. Embedding lookup
- B. Cleaning, normalization, and structured extraction (URLs, emails, dates) before deeper processing
- C. Computing cross-entropy
- D. Backpropagation

> [!success]- Answer
> **B.** Regex is a feature-engineering tool that runs *before* learned models, not a substitute for them.

**11.** The pattern `[^\s]+@[^\s]+\.[^\s]+` to match emails will:
- A. Fail on every email
- B. Match many non-emails too (e.g., *"foo@bar.baz!"* with trailing punctuation included)
- C. Always be optimal
- D. Reject Unicode

> [!success]- Answer
> **B.** Naive email regexes overmatch and need careful boundaries; the full RFC 5322 email regex is famously complex.

**12.** `re.findall(r"(\w+)\s\1", "the the cat cat")` returns:
- A. `['the', 'cat']` via the backreference `\1`
- B. `['the the', 'cat cat']`
- C. `[]`
- D. `['the', 'the', 'cat', 'cat']`

> [!success]- Answer
> **A.** `\1` references group 1; the regex matches consecutive duplicate words and `findall` returns the captured group only.

**13.** Which use of regex *would* be defensible inside a modern Transformer-based pipeline?
- A. Replacing the model entirely
- B. Pre-stripping boilerplate (HTML tags, URLs) before the subword tokenizer sees the text
- C. Computing embeddings
- D. Computing softmax

> [!success]- Answer
> **B.** Regex remains a sharp tool for deterministic surface-level cleanup — even in deep pipelines.

**14.** `\d+` against *"abc"* returns:
- A. `["abc"]`
- B. No match (`[]` from `findall`)
- C. `["0"]`
- D. Error

> [!success]- Answer
> **B.** No digits, no match.

**15.** `(?:abc)` differs from `(abc)` in that:
- A. It is a *non-capturing* group — used to group without storing the match
- B. It anchors the match
- C. It is case-insensitive
- D. It enables greedy matching

> [!success]- Answer
> **A.** Non-capturing groups exist for grouping/alternation without polluting the capture indices.

**16.** Anchoring `^` matches the start of:
- A. The string by default; the start of *each line* if `re.MULTILINE` is enabled
- B. Every word
- C. Every match
- D. The capture group

> [!success]- Answer
> **A.** Default mode anchors once at string start; MULTILINE re-anchors at every line break.

**17.** `\D` matches:
- A. Any digit
- B. Any non-digit character — the complement of `\d`
- C. Any whitespace
- D. The literal character *D*

> [!success]- Answer
> **B.** Capital-letter classes negate the lowercase ones: `\D = [^\d]`, `\W = [^\w]`, `\S = [^\s]`.

**18.** A reasonable regex to extract `#hashtags` from *"loving #NLP and #Regex_101!"* is:
- A. `\w+` (matches all words)
- B. `#\w+` (captures the `#` prefix and the word body)
- C. `[a-z]+`
- D. `\b\w+\b`

> [!success]- Answer
> **B.** The literal `#` plus `\w+` cleanly captures the hashtag including the prefix.

**19.** What is the danger of using `.*` over multi-line input without the DOTALL flag?
- A. `.` does not match newlines, so the regex stops at line breaks unless `re.DOTALL` is set
- B. It always matches newlines
- C. It crashes the engine
- D. It changes encoding

> [!success]- Answer
> **A.** Default `.` excludes `\n`; for "match across lines" you need `re.DOTALL`/`re.S`.

**20.** Why is sentence segmentation a poor fit for regex alone?
- A. Periods are ambiguous — abbreviations (*Dr.*, *e.g.*), decimals (*3.14*), and ellipses break naive `\.` rules
- B. Sentences cannot be matched
- C. Periods don't exist in some languages
- D. Regex cannot count

> [!success]- Answer
> **A.** Real sentence segmentation requires a model trained on contextual cues; regex handles the easy 80% and fails on the long tail.

**21.** The cleanest single advantage of regex over CFGs is:
- A. Greater expressive power
- B. Engine speed and ubiquity for shallow surface-level extraction; the trade is that regex is strictly weaker (regular languages only)
- C. Native support for tree structures
- D. Built-in semantics

> [!success]- Answer
> **B.** Regex sits at the bottom of Chomsky's hierarchy — fast and ubiquitous, but strictly less expressive than CFGs.

**22.** *"Use regex to extract phone numbers"* in international form is fragile because:
- A. Phone numbers vary in length, separators, and country code conventions — a single regex over-/under-matches across regions
- B. Regex cannot match digits
- C. Phone numbers are not strings
- D. Lookarounds are required

> [!success]- Answer
> **A.** Format heterogeneity is the killer; libraries like `phonenumbers` exist precisely to handle the long tail regex cannot.
