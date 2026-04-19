**Tags:** #concept #rl
**Related:** [[Advanced RL Techniques]], [[World Models]], [[Active Inference]]

## Definition

JEPA (Joint-Embedding Predictive Architecture) is a system architecture for autonomous machine intelligence proposed by Yann LeCun (2022). It is a world model architecture that learns compact, abstract representations of world states and predicts future states in that latent space — enabling planning at the level of abstractions rather than raw observations.

> [!info] Key Intuition
> JEPA separates *encoding* (compressing observations into abstract representations) from *prediction* (reasoning about what comes next in abstract space) from *acting* (selecting actions to minimise cost). This mirrors how humans plan: not by imagining every pixel of the future, but by reasoning about abstract consequences of actions.

## System Architecture

JEPA comprises six interconnected modules:

| Module | Role |
|---|---|
| **Configurator** | Sets goals and parameters for other modules |
| **World Model** | Predicts future abstract states |
| **Short-term memory** | Stores recent states and predictions |
| **Perception** | Encodes observations into abstract representations |
| **Actor** | Proposes action sequences |
| **Critic / Cost** | Evaluates predicted state sequences; Intrinsic cost drives exploration |

## Two Operating Modes

**Mode-1 (Reactive/Habitual)**:
$$x \xrightarrow{\text{Enc}} s[0] \xrightarrow{\text{Actor}} a[0] \to \text{environment}$$
The actor maps directly from encoded state to action. Fast, low-resource, habitual.

**Mode-2 (Deliberate/Planning)**:
$$s[0] \xrightarrow{\text{Pred}(s,a)} s[1] \xrightarrow{\text{Pred}(s,a)} \cdots \xrightarrow{\text{Pred}(s,a)} s[T]$$

The world model unrolls a sequence of predicted states $s[0], \ldots, s[T]$; the actor proposes actions $a[0], \ldots, a[T]$; an optimisation procedure finds the action sequence that minimises total cost $\sum_t C(s[t])$. This is model-predictive control with receding horizon, implemented in latent space.

The key identity: $s[t+1] = \text{Pred}(s[t], a[t])$ — the world model's predictor generates the sequence.

## Training a Reactive Policy from Mode-2

Mode-2 is computationally expensive (requires running the world model $T$ steps for every candidate action sequence). To amortise this:
1. Run Mode-2 to produce an optimal action sequence $\hat{a}[0], \ldots, \hat{a}[T]$
2. Train the actor $A(s[t])$ to minimise divergence $D(A(s[t]), \hat{a}[t])$
3. The actor becomes a **reactive approximation** to Mode-2 planning — producing Mode-2-quality actions at Mode-1 speed

## OaK Architecture (Alberta Plan)

Sutton, Bowling & Pilarski (2022) propose a complementary architecture for **continual learning** in open-ended environments, built on four loosely coupled processes:

1. **Perception** — constructing state features
2. **Play** — intrinsically-motivated problem posing and solving
3. **Prediction** — learning predictive knowledge (transition models)
4. **Planning** — improving values and policies throughout

The STOMP progression links them: State features → Subtasks → Options/values → Models of options. Feedback from planning continually directs feature construction, forming a self-improving loop.

> [!example]- JEPA vs Dreamer
> Both JEPA and Dreamer use a learned world model for planning in latent space. The key difference: Dreamer (DreamerV2/V3) learns a probabilistic RSSM with discrete latents trained end-to-end on reconstruction; JEPA emphasises *joint embeddings* trained by self-supervised energy minimisation (no pixel-level reconstruction required). JEPA is intended to scale to video understanding and open-ended physical reasoning, where pixel reconstruction is wasteful and costly.

> [!warning] Common Misconception
> JEPA does not predict in pixel space. The predictor operates on abstract latent representations $s[t]$, not raw observations. This avoids the "prediction in pixel space is hard" problem: irrelevant details (textures, lighting) need not be predicted, only the abstract dynamics that matter for planning and control.

## Significance

JEPA represents a fundamental shift in how world models are designed: from reconstructing observations to predicting abstract representations. Combined with the Mode-1/Mode-2 distinction (reactive habit vs deliberate planning), it offers a computational architecture that mirrors dual-process theories of cognition and scales to complex, open-ended environments.
