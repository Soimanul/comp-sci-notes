**Tags:** #concept #llm #nlp
**Related:** [[Context Window Limitations]], [[Transformer Architecture]], [[Self-Attention]]

## Definition
Large Context Models (LCMs) are Transformer language models that extend the context window from the typical few thousand tokens to hundreds of thousands or even millions:
$$T \longrightarrow T' \quad \text{with } T' \gg T$$
Attention is then computed over a much larger window:
$$\alpha_{ij} = \mathrm{softmax}\!\left(\frac{q_i k_j^\top}{\sqrt{d_k}}\right), \quad j \in \{t - T', \dots, t - 1\}$$

> [!info] Key Intuition
> LCMs do not change the architecture in spirit — they just enlarge the window. The hard problem shifts from *getting access to enough information* to *allocating attention well across a much larger pool*.

## Why Larger Helps
- More long-range dependencies become representable inside a single forward pass.
- Whole books, codebases, or transcripts can be processed without external retrieval.
- Few-shot prompts can include far more examples.

## Why Larger Is Not a Free Lunch
- **Quadratic cost** ($\mathcal{O}(T'^2)$) — extra engineering (ring/flash attention, sparse patterns) is required to make this tractable.
- **Attention dilution** — the same softmax now spreads over many more keys; the model must learn to focus despite this.
- **Training data shift** — the model needs training examples that actually exercise long-range structure; otherwise the long context is unused.

> [!example]- Worked Example
> Models like Gemini 1.5 (1M+ tokens) and Claude with extended context are LCMs. They can ingest entire codebases or hours of transcripts in a single call, replacing many RAG-style chunking pipelines for tasks where context is bounded and reusable.

> [!warning] Common Misconception
> "Bigger context = better answers" is not automatic. Without good training and positional encodings (e.g. RoPE scaling, YaRN, ALiBi), models with long advertised windows still degrade on inputs much shorter than their nominal limit.

## Significance
LCMs reframe the limits of monolithic LLMs: with a wide enough window, retrieval becomes optional for many tasks. The remaining bottleneck is no longer access but *effective allocation* of attention across enormous inputs.
