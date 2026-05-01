**Tags:** #concept #llm #nlp
**Related:** [[Transformer Architecture]], [[Self-Attention]], [[Large Context Models]]

## Definition
The context window is the maximum number of tokens a Transformer can attend to in one forward pass. Predictions are conditioned only on the last $T$ tokens:
$$p_\theta(w_t \mid w_{t-T}, \dots, w_{t-1})$$
Both quality and cost suffer as we approach this limit.

> [!info] Key Intuition
> Attention has finite reach in two senses: hard (you literally cannot feed more tokens than the window allows) and soft (even within the window, attention spread thin across many tokens loses focus on what matters).

## Two Constraints

### 1. Computational Cost
Self-attention is quadratic in sequence length:
$$\text{cost} = \mathcal{O}(T^2 \cdot d)$$
Doubling the context quadruples the compute and memory required for the attention layer.

### 2. Attention Dilution
Attention weights:
$$\alpha_{ij} = \frac{\exp(q_i^\top k_j)}{\sum_{j'} \exp(q_i^\top k_{j'})}$$
sum to 1 over all $T$ keys. As $T$ grows, each individual weight shrinks on average, making it harder for the model to concentrate on the truly relevant positions.

> [!example]- Worked Example
> A model with $T = 4{,}096$ asked to summarise a 100-page document either truncates (loses information) or chunks the document and summarises pieces (loses cross-chunk dependencies). Even an extension to $T = 128{,}000$ does not guarantee the model effectively uses the middle of the prompt — empirically, "lost in the middle" failures appear well before the hard limit.

> [!warning] Common Misconception
> A larger advertised context window does *not* mean uniformly better performance over that window. Effective use of long context is its own research problem; specialised positional encodings (RoPE, ALiBi) and training recipes are needed to make distant tokens count.

## Significance
The context window is one of the two structural limits of monolithic LLMs (the other being static, training-time-fixed knowledge). RAG, agentic loops, and long-context architectures (LCMs) all exist to push past it.
