**Tags:** #hub #nlp #pos #sequence-labelling
**Related:** [[Natural Language Processing]], [[Markov Assumption]], [[Named Entity Recognition]]

## Overview

Part-of-Speech (POS) tagging assigns a grammatical category (noun, verb, adjective, etc.) to each token in a sentence. It is a foundational NLP preprocessing step that enables parsing, named entity recognition, and many downstream tasks.

> [!abstract]- TL;DR
> POS tagging is a sequence-labelling problem: each word receives a tag from a closed tagset. Classical systems used HMM with Viterbi decoding; modern systems use neural architectures that encode context bidirectionally and eliminate the Markov independence assumption.

## Knowledge Map

### 1. Tag Sets
- [[Penn Treebank POS Tagset]]
- [[Universal POS Tags]]

### 2. Classical Approaches
- [[HMM-Based POS Tagger]]
- [[Viterbi Algorithm]]

### 3. Neural Approaches
- [[Neural POS Tagger]]

> [!question]- Common Exam Questions
> - What are the emission and transition probabilities in an HMM tagger?
> - Trace through the Viterbi algorithm for a short sentence.
> - How do neural taggers overcome the Markov assumption of HMMs?
> - What is the difference between the Penn Treebank tagset and Universal POS tags?
