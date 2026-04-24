**Tags:** #concept #llm
**Related:** [[KV Caching]], [[Paged Attention]], [[LLM Quantization]]

## Definition

**Speculative decoding** is an inference acceleration technique where a small, fast **draft model** generates a candidate sequence of $\gamma$ tokens, and the large **target model** verifies all $\gamma$ tokens in parallel (one forward pass), accepting or rejecting them based on a probabilistic criterion — achieving target model quality at draft model speed.

> [!info] Key Intuition
> The bottleneck in autoregressive LLM inference is that each token requires a full forward pass. Speculative decoding says: use a small cheap model to guess the next few tokens, then use the big model to check all guesses at once. One large-model forward pass either accepts multiple tokens or corrects the first error — on average generating $>1$ token per large-model call.

## Algorithm

**Step 1 (Draft):** Draft model $M_q$ autoregressively generates $\gamma$ candidate tokens $x_1, \ldots, x_\gamma$ with probabilities $q(x_i | x_{<i})$.

**Step 2 (Verify):** Target model $M_p$ runs a single forward pass over $[x_{1}, \ldots, x_\gamma]$, computing $p(x_i | x_{<i})$ for all positions simultaneously.

**Step 3 (Accept/Reject):** For each token $x_i$ from left to right:
$$P(\text{accept}\ x_i) = \min\left(1, \frac{p(x_i | x_{<i})}{q(x_i | x_{<i})}\right)$$

- If accepted, move to next token
- If rejected, sample from adjusted distribution $p' \propto \max(0, p - q)$ and discard remaining draft tokens

**Step 4:** If all $\gamma$ tokens accepted, sample one more token from $M_p$.

## Key Property

The acceptance criterion guarantees the **output distribution is identical to $M_p$** — speculative decoding introduces no quality degradation. It is an exact method.

## Speed-up

Expected tokens per large-model forward pass:
$$\mathbb{E}[\text{accepted tokens}] = \frac{1 - \alpha^{\gamma+1}}{1 - \alpha}$$

where $\alpha$ = average acceptance rate. For $\alpha = 0.8, \gamma = 5$: expected acceptance ≈ 3.3 tokens per call.

## Draft Models

| Approach | Draft model |
|---|---|
| External small model | Smaller model in same family (e.g. LLaMA 3 8B drafts for 70B) |
| Self-speculative (Medusa) | Draft heads attached to the target model itself |
| n-gram lookup | Retrieve candidate tokens from the current context |

> [!example]- Speedup in Practice
> Llama-2 70B with Llama-2 7B as draft: ~2.5× inference speedup at identical output quality.

## Significance

Speculative decoding achieves 2–3× LLM inference throughput improvements with zero quality loss, making it one of the most practically impactful inference optimisations available today. It is implemented in HuggingFace, vLLM, and TGI.
