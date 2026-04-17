**Tags:** #concept #nlp #pos #sequence-labelling
**Related:** [[POS Tagging]], [[HMM-Based POS Tagger]], [[Word Embeddings]]

## Definition

A neural POS tagger encodes each token using distributed representations (embeddings + context encoder) and predicts its tag via a softmax classifier, optionally adding a CRF layer for global sequence consistency. Neural taggers outperform HMMs by encoding full bidirectional context without the Markov assumption.

> [!info] Key Intuition
> A BiLSTM or Transformer encoder "sees" the entire sentence simultaneously before making any tag decision — overcoming the HMM's one-step-back horizon.

## Core Mechanics

Standard architecture:
1. **Character CNN / subword embedding** → handles OOV and morphology
2. **Word embedding** (pretrained or learned from scratch)
3. **BiLSTM encoder** → hidden state $\mathbf{h}_i$ encodes left and right context at each position
4. **Linear layer** → scores per tag for each position
5. **CRF layer** (optional) → models tag transition probabilities globally; trained with forward algorithm, decoded with Viterbi

With a CRF layer the model learns that "NN followed by VBZ" is more likely than "VBZ followed by VBZ", adding the same global constraints as HMMs but on top of rich neural features.

> [!example]- Worked Example
> BERT fine-tuned for POS tagging: attach a linear classification head to each [CLS]-stripped token output. Fine-tune on Penn Treebank. State-of-the-art accuracy (~97.8%) with no explicit feature engineering.

## Significance

Near-human POS accuracy is now achieved by fine-tuning pretrained Transformers. The remaining errors are primarily on genuinely ambiguous cases that require world knowledge (e.g., "They can can the fish" — both "can"s are ambiguous).
