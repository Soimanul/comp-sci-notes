**Tags:** #concept #rl
**Related:** [[Advanced RL Techniques]], [[State Value Function]], [[Action Value Function]], [[Intrinsic Rewards]]

## Definition

Universal Value Function Approximators (UVFAs) extend standard value function approximators to generalise over both states and goals simultaneously. Rather than learning $V(s; \theta)$ for a fixed reward function, UVFAs learn:

$$V(s, g; \theta)$$

where $g$ is a goal specification, allowing a single neural network to represent value functions for an entire family of tasks.

> [!info] Key Intuition
> A UVFA is to value functions what multi-task learning is to supervised models: instead of training a separate policy for each goal, you train one network that has learned the *structure* of how goals relate to values — so it generalises to unseen goals at test time.

## Architecture

A naive approach concatenates $[s, g]$ as input to a single network. The UVFA paper (Schaul et al. 2015) proposes a **two-stream architecture** that exploits the factored structure:
- **State encoder** $\phi(s)$: maps state to embedding
- **Goal encoder** $\psi(g)$: maps goal to embedding
- **Combiner** $h$: merges both embeddings to produce $V(s, g; \theta)$

This factored architecture allows efficient supervised learning: target embeddings are first derived by matrix factorisation of observed $(s, g, V)$ triples, then the two encoders are trained to predict these embeddings.

## Generalised Value Functions

Formally, a generalised value function for goal $g$ and policy $\pi$:

$$V_{g,\pi}(s) := \mathbb{E}\left[\sum_{t=0}^\infty R_g(s_{t+1}, a_t, s_t) \prod_{k=0}^t \gamma_g(s_k) \;\middle|\; s_0 = s\right]$$

where both the reward $R_g$ and discount $\gamma_g$ may depend on the goal. This subsumes standard value functions as the special case where $g$ is fixed.

## Role in Never Give Up

UVFAs are the key architectural choice in Never Give Up (NGU): the agent uses a UVFA to **simultaneously learn many directed exploration policies** with different trade-offs between exploration and exploitation. By parameterising the exploration-exploitation trade-off as part of the goal $g$, a single neural network can transfer knowledge from predominantly exploratory policies to build effective exploitative policies — without retraining from scratch for each setting.

> [!example]- Goal Generalisation in Robotic Reaching
> An agent trained on goals sampled from one region of object positions can, with a UVFA, generalise to goals in other regions it has never seen. The state encoder learns a representation of "how far from various reference points this state is" and the goal encoder learns "what position is being targeted" — combining these gives value estimates that interpolate smoothly across the goal space.

> [!warning] Common Misconception
> A UVFA does not require goals to be positions or object states. Goals are arbitrary vectors — they can represent desired reward functions, desired terminal states, or any task descriptor. The architecture generalises over whatever family of tasks the goal embedding encodes.

## Significance

UVFAs are foundational for multi-task and goal-conditioned RL, enabling reuse of a single policy across many tasks. They are also the mechanism that allows Never Give Up and Agent57 to scale directed exploration across many distinct behavioural modes with a single shared network.
