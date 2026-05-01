**Tags:** #concept #nlp #llm
**Related:** [[Transformer Architecture]], [[Sequence Language Modelling]], [[RAG Pipeline]]

## Definition
A Transformer language model defines a single mechanism — autoregressive next-token prediction:
$$p_\theta(w_1, \dots, w_T) = \prod_{t=1}^T p_\theta(w_t \mid w_1, \dots, w_{t-1})$$
Different NLP tasks reduce to *different ways of formatting the input and interpreting the output* of this same mechanism, rather than to different models.

> [!info] Key Intuition
> The model is task-agnostic. The task lives in the prompt. Reframe the input correctly and a generic next-token predictor handles classification, QA, and summarisation with the same forward pass.

## Three Reductions

| Task | Input format | Output interpretation | Formal goal |
|---|---|---|---|
| **Classification** | sentence + label set $\mathcal{Y} = \{y_1, \dots, y_k\}$ | predicted continuation = label | $\hat{y} = \arg\max_{y_i \in \mathcal{Y}} p_\theta(y_i \mid x)$ |
| **Question answering** | context $c$ + question $q$ | generated answer sequence | $\hat{a} = \arg\max_a p_\theta(a \mid q, c)$ |
| **Summarisation** | long document $x$ + instruction | shorter generated sequence | $\hat{s} = \arg\max_s p_\theta(s \mid x)$ |

In each case the model produces $\arg\max_{w_1, \dots, w_T} p_\theta(w_1, \dots, w_T \mid x)$; only the admissible output set $\{w_t\}$ and the way we read it differ.

> [!example]- Worked Example
> "Classify the review as positive or negative: *The food was great.* →" — the model outputs probabilities for many tokens; we restrict attention to {positive, negative} and pick the higher-probability one. No classifier head, no extra training, just prompt engineering.

> [!warning] Common Misconception
> The model is not "really doing" classification or summarisation in the symbolic sense — there is no explicit class boundary, no compression metric. The behaviour emerges statistically from training distributions where summaries are shorter, labelled examples follow a template, etc.

## Significance
This unified view is the conceptual core of modern LLM usage: the same model serves as classifier, retriever, summariser, and translator. It also explains why prompt engineering matters so much — the prompt *is* the task definition.
