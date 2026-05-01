**Tags:** #concept #nlp #language-models
**Related:** [[Statistical Language Models]], [[Recurrent Neural Networks]], [[Text Generation with RNNs]]

## Definition
A sequence language model assigns a probability to the next token given all preceding tokens:
$$p_\theta(w_{t+1} \mid w_1, w_2, \dots, w_t)$$
The model learns parameters $\theta$ that maximize the likelihood of observed sequences — equivalently, that minimize the negative log-likelihood (cross-entropy).

> [!info] Key Intuition
> A language model is a function that, given a context, scores how plausible each possible next word is. Everything else — generation, classification, embedding — can be built on top of this single conditional distribution.

## Why Sequences Matter
Word order changes meaning: "dog bites man" and "man bites dog" share the same bag of words but differ semantically. Models that ignore order (Bag-of-Words, TF–IDF) cannot represent this distinction; sequence models can.

Typical sequential data:
- Natural language sentences
- Speech signals
- Time series
- DNA sequences

> [!example]- Worked Example
> Vocabulary {I, like, natural, language, processing, EOS}. After feeding "I", a trained RNN might output:
> - $p(\text{like} \mid \text{I}) = 0.181$
> - $p(\text{natural} \mid \text{I}) = 0.185$
> - $p(\text{processing} \mid \text{I}) = 0.183$
>
> Training adjusts the parameters so that the probability mass concentrates on the actually-observed next token in the corpus.

## Significance
The next-token objective is the unifying training signal behind virtually all modern NLP, from Elman RNNs to GPT-style transformers. Mastering this view makes architecture choices look like trade-offs in *how* to compute the same probability rather than fundamentally different models.
