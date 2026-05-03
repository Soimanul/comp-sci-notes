**Tags:** #concept #nlp #pos
**Related:** [[POS Tagging]], [[Context-free grammar - CFG]], [[POS as Structured Prediction]]

## Definition

Early computational linguistics treated language as a rule-governed symbolic system. POS tags were assigned by:

- a **lexicon** mapping each word to its possible categories,
- **handcrafted disambiguation rules**,
- **complete and consistent grammars** (e.g. CFG productions like $S \to NP\, VP$).

Under this view, grammatical category is determined by rule derivation. The approach fails because natural language is inherently ambiguous and grammars only specify well-formedness, not probability.

> [!info] Key Intuition
> A grammar tells you what is *possible*; a probabilistic model tells you what is *likely*. Real text needs the latter.

## The Ambiguity Problem

The same word frequently belongs to different categories depending on context:

| Sentence | Token *"can"* | Tag |
|---|---|---|
| *"They can fish"* | modal verb | MOD |
| *"They bought a can of fish"* | noun | NOUN |

Similarly *"fish"* in the first sentence is a verb and in the second a noun. **Category assignment depends on context, not on the word alone**.

## Why the Rule Approach Collapses

- **Exhaustive lexicons are infeasible**: language variability grows unbounded; new words and senses keep appearing.
- **Disambiguation rules conflict**: rules added to fix one case break another.
- **Grammar maintenance is brittle**: consistency across tens of thousands of rules is hard to verify and easy to break.
- **No probabilistic ranking**: when multiple parses are valid, rules cannot prefer one.

## Significance

The collapse of rule-based tagging is the historical motivation for the **probabilistic turn** in NLP. Once you accept that ambiguity is the rule rather than the exception, the question shifts from "what are the grammar rules?" to "what is the most likely tag sequence given these words?" — which is exactly the framing of [[POS as Structured Prediction]] and the [[HMM-Based POS Tagger]].

> [!warning] Common Misconception
> Rule-based components are not gone — modern industrial pipelines often combine learned models with handwritten rules for closed-class words, dates, and currency. The collapse was of *purely* rule-based tagging, not of rules as a tool.
