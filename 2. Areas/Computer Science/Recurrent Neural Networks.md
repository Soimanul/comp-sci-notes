**Tags:** #topic #hub #nlp
**Related:** [[Neural Networks for NLP]], [[Natural Language Processing]]

## Overview
Recurrent Neural Networks (RNNs) extend feedforward networks to ordered data. By maintaining an internal hidden state that is updated at every time step, an RNN models sequences of arbitrary length and exposes the conditional distribution $p(w_{t+1} \mid w_1, \dots, w_t)$ used in language modelling. This hub covers the Elman cell, the role of hidden states, training via backpropagation through time, and the practical limits that motivate more advanced architectures like LSTMs and Transformers.

> [!abstract]- TL;DR
> An RNN reads a sequence one token at a time and threads a hidden state from step to step, so each output depends on all preceding inputs. They train via backpropagation through time, but vanishing/exploding gradients limit their effective context to roughly 5–10 tokens.

## Knowledge Map

### 1. Sequences and Language Modelling
- [[Sequence Language Modelling]]

### 2. The Elman RNN
- [[Elman RNN]]
- [[Hidden State (RNN)]]

### 3. Training
- [[Backpropagation Through Time]]
- [[Vanishing and Exploding Gradients]]

### 4. Using RNNs
- [[RNN Task Configurations]]
- [[Text Generation with RNNs]]
- [[Long-Range Dependencies in RNNs]]

> [!question]- Common Exam Questions
> - Why does an RNN have only one cell even though the unfolded diagram shows many?
> - Where does the vanishing/exploding gradient problem come from mathematically?
> - Compare many-to-one, one-to-many, and many-to-many RNN configurations with examples.
> - How does an RNN generate text after training is complete?
