**Tags:** #hub #nlp #pos #sequence-labelling
**Related:** [[Natural Language Processing]], [[Markov Assumption]], [[Named Entity Recognition]]

## Overview

Part-of-Speech (POS) tagging assigns a grammatical category (noun, verb, adjective, …) to each token in a sentence. It is the structural layer in the NLP pipeline that comes after tokenisation and morphological analysis and before syntactic parsing. Conceptually, POS tagging extends classifier ideas (Naïve Bayes, logistic regression) into the **structured prediction** regime, where the predictions at different positions are not independent.

> [!abstract]- TL;DR
> POS tagging is structured prediction: predict an entire tag sequence rather than independent labels. Rule-based systems collapse under ambiguity; classical statistical solutions use HMM with Viterbi decoding; modern systems use neural taggers. The conceptual machinery — conditional probabilities, smoothing, likelihood maximisation — is identical to Naïve Bayes; only the **interdependence across positions** is new.

## Knowledge Map

### 1. The Problem
- [[POS as Structured Prediction]]
- [[Limits of Rule-Based Tagging]]

### 2. Tag Sets
- [[Penn Treebank POS Tagset]]
- [[Universal POS Tags]]

### 3. Classical Probabilistic Approach
- [[HMM-Based POS Tagger]]
- [[Viterbi Algorithm]]
- [[What HMM Captures and Misses]]

### 4. Neural Approaches
- [[Neural POS Tagger]]

> [!question]- Common Exam Questions
> - Why is POS tagging a structured prediction problem and not just a classification problem?
> - State the two HMM independence assumptions and the resulting joint probability.
> - Trace Viterbi for *"They can fish"* given a small transition/emission table.
> - What does the HMM tagger explicitly fail to capture that a Transformer does not?
> - Why do rule-based taggers fail on natural language ambiguity?
