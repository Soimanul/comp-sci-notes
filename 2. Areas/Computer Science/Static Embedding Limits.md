**Tags:** #concept #nlp #embeddings
**Related:** [[Word Embeddings]], [[Word2Vec]], [[Attention Mechanism]], [[Transformer Architecture]]

## Definition

A **static embedding** assigns one fixed vector per word **type**, regardless of context. Word2Vec, GloVe, and fastText are all static. This is also the structural ceiling that motivated the move to **contextual** representations (ELMo, BERT, GPT) built on attention.

> [!info] Key Intuition
> A single vector per word cannot represent multiple senses simultaneously. The vector ends up being a **weighted average** of the senses present in the training corpus — useful, but blunt.

## What Static Embeddings Cannot Capture

### Polysemy and Homonymy
*"bank"* receives one vector that mixes the financial and river senses. The geometry near *"bank"* contains both *"loan"* and *"river"*, but no single document ever activates both.

### Context-Dependent Meaning
Sense, register, and pragmatic role shift with context: *"break a leg"* (idiom) vs *"break a leg"* (literal). Static vectors cannot reflect this.

### Long-Range Composition
Embeddings are word-level. Sentence and paragraph meaning must be reconstructed downstream — by averaging, RNN composition, or attention.

### Out-of-Vocabulary Morphology
Word-level static models like Word2Vec cannot embed unseen words at all. fastText partially fixes this with character n-grams, but the underlying type-level limit remains.

## The Solution: Context-Dependent Representations

To move beyond static embeddings, the representation of a word must **depend dynamically on its context**:

$$v_w \;\;\rightarrow\;\; v_w^{(c)}$$

This is the conceptual leap to:

- **ELMo** — contextual vectors from a bidirectional LSTM.
- **BERT / GPT** — transformer encoders/decoders where attention recomputes each token's representation conditional on every other token.

In these models, the vector for *"bank"* in *"river bank"* and *"savings bank"* is genuinely different.

> [!warning] Common Misconception
> "BERT replaces Word2Vec." BERT's input layer still uses static embeddings (subword) — what changes is that attention layers transform them into context-sensitive representations. The static layer is the start of the pipeline, not its rival.

## Significance

Recognising this limit is the conceptual hinge between Module 3 and Module 4 of the NLP curriculum: static embeddings exhaust what local prediction over a fixed window can do, and contextual transformer representations are the natural next step.
