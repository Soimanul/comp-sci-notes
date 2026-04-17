**Tags:** #hub #nlp #ner #sequence-labelling
**Related:** [[Natural Language Processing]], [[POS Tagging]], [[BIO Tagging Scheme]]

## Overview

Named Entity Recognition (NER) locates and classifies named entities in text into predefined categories such as person, organization, location, date, and quantity. It is typically framed as a sequence-labelling problem with a BIO or BIOES tagging scheme applied over tokens.

> [!abstract]- TL;DR
> NER finds spans of text that refer to real-world entities and classifies them. Modern systems use BERT-based token classifiers with BIO tagging that achieve near-human performance, replacing earlier CRF-over-features pipelines.

## Knowledge Map

### 1. Tagging Schemes
- [[BIO Tagging Scheme]]
- [[BIOES Tagging Scheme]]

### 2. Classical Approaches
- [[CRF for Sequence Labelling]]

### 3. Neural / Transformer Approaches
- [[BERT for NER]]

> [!question]- Common Exam Questions
> - What is the difference between BIO and BIOES tagging schemes for NER?
> - Why is NER harder than POS tagging?
> - How does a CRF layer improve over a simple softmax for sequence labelling?
> - What makes BERT-based NER more effective than CRF-based systems?
