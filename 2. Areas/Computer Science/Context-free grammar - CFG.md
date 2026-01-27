**Tags:** #concept #nlp #formal-languages #cfg  
**Related:** [[Formal Language Theory]] · [[Chomsky and formal language theory]] · [[CFG derivation example]]

## Definition
A context-free grammar is a rule system that generates sentences by repeatedly rewriting non-terminal symbols into sequences of terminals and non-terminals.

## Core components
- **Non-terminals:** abstract categories (e.g., S, NP, VP, PP).
- **Terminals:** observable tokens (words).
- **Production rules:** expansions of the form  
  $$
  A \rightarrow \alpha
  $$
  where $A$ is a single non-terminal and $\alpha$ is a sequence of terminals/non-terminals.
- **Start symbol:** the root category from which derivations begin.

## What CFGs capture
- Hierarchical phrase structure (constituents).
- Recursion and nesting (theoretically unbounded structures).
- Syntactic well-formedness defined by derivability under the grammar.
