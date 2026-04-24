**Tags:** #concept #llm
**Related:** [[RLHF]], [[Fine-tuning in NLP]], [[PPO for LLM Alignment]]

## Definition

**RLHF vs Cross-Entropy Training** compares the standard supervised language model training objective (maximise likelihood of training tokens) with RLHF's reinforcement learning objective (maximise human preference reward), highlighting why RLHF is needed for alignment even when cross-entropy training on demonstrations is available.

## Cross-Entropy (Supervised) Training

**Objective:** Maximise the log probability of the training text:
$$L_{CE} = -\sum_{t} \log P_\theta(w_t | w_{<t})$$

**What it learns:** Imitate the training distribution — produce text that looks like training examples.

**Limitations for alignment:**
| Problem | Description |
|---|---|
| Exposure bias | At inference, the model conditions on its own outputs (not training text), creating distribution shift |
| Imitation not preference | The model imitates good AND bad examples in demonstrations |
| Cannot express negative feedback | CE only pushes up probability of desired outputs; cannot push down bad outputs |
| Overfit to demonstrations | Memorises formats rather than learning generalizable helpfulness |

## RLHF Training

**Objective:** Maximise expected reward from a preference model, minus KL divergence from the supervised model:
$$L_{RLHF} = \mathbb{E}[r_\phi(x, y)] - \beta \, \text{KL}(\pi_\theta \| \pi_{\text{ref}})$$

**What it adds:**
| Advantage | Description |
|---|---|
| Contrastive signal | Explicitly pushes bad responses down, good responses up |
| Generalisable preferences | Learns what humans prefer, not just what they demonstrated |
| Coverage of unseen prompts | RL exploration can improve on prompts not in the demo set |
| Calibrated uncertainty | The KL penalty prevents degenerate solutions |

## When Is CE Sufficient?

CE (SFT) alone can be enough when:
- Demonstrations are high-quality and representative
- The task has a clear correct answer (code correctness, factual QA)
- Model scale is large enough to learn from demonstrations

RLHF is needed when:
- Human preferences are subjective or hard to demonstrate
- The task requires balancing multiple competing objectives (helpfulness vs. safety)
- Dealing with open-ended generation where many valid outputs exist

## Significance

The SFT → RM → PPO pipeline of RLHF addresses the fundamental limitations of imitation learning for building aligned AI assistants. Understanding this distinction explains why leading LLM providers invest heavily in RLHF infrastructure.
