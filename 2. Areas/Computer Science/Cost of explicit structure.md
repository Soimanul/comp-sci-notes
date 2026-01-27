**Tags:** #concept #nlp #tradeoffs #symbolic  
**Related:** [[Two Ways of Thinking About Language]] · [[Symbolic view of language]] · [[Statistical view of language]] · [[NLP libraries encode assumptions]]

## Definition
The cost of explicit structure is the practical overhead of representing language with detailed hand-specified rules and symbolic formalisms, including the engineering effort, brittleness, and scalability limits that come with maintaining those structures.

## Why it becomes expensive
- **Coverage problem:** real language exhibits variation, ambiguity, exceptions, and domain-specific usage that is hard to enumerate with rules.
- **Brittleness:** small deviations (typos, informal syntax, novel constructions) can break rule-based analyses.
- **Maintenance burden:** grammars and rule systems must be continuously updated to handle new phenomena and domains.
- **Scaling limits:** high-quality symbolic resources require expert design and do not scale as easily as data-driven learning.

## Consequence for modern NLP
Because explicit structure is costly to build and keep correct at scale, many modern systems approximate structure statistically, accepting reduced interpretability in exchange for robustness and empirical performance.
