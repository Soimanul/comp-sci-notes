**Tags:** #concept #rl
**Related:** [[Actor-Critic]], [[Actor-Critic Methods]], [[Asynchronous Advantage Actor-Critic (A3C)]], [[Advantage Function]], [[Generalized Advantage Estimation]]

## Definition

Advantage Actor-Critic (A2C) is a synchronous, on-policy actor-critic algorithm that uses the [[Advantage Function]] as the critic signal. The policy gradient becomes:

$$\nabla_\theta J(\theta) = \mathbb{E}_{\pi_\theta}\!\left[\nabla_\theta \log\pi_\theta(s, a)\, A^w(s, a)\right]$$

where $A^w(s,a) = Q^w(s,a) - V^w(s)$ is the estimated advantage.

> [!info] Key Intuition
> A2C is the synchronous, deterministic version of A3C: all parallel workers complete their segment of experience, then the global network is updated at once — making it GPU-friendly and empirically comparable to A3C in performance.

## Architecture

A2C typically uses a single neural network with shared convolutional layers that output both:
- The policy distribution $\pi_\theta(a|s)$ (actor head, softmax output).
- The state-value estimate $V(s; \theta_v)$ (critic head, linear output).

Multiple workers run in parallel environments, but unlike A3C they do not send asynchronous gradient updates — they collect experience and update synchronously.

## How It Relates to A3C

A3C (Mnih et al., 2016) is the asynchronous variant: multiple workers update a global network concurrently without waiting for each other, effectively parallelising stochastic gradient descent. A2C is a synchronous alternative that:
- Waits for all workers to finish their segment before updating.
- Averages gradients across workers.
- More effectively utilises GPUs due to larger batch sizes.

Empirically, OpenAI researchers found A2C produces comparable performance to A3C while being more efficient and simpler to implement.

> [!example]- A2C Update Step
> With $n$ parallel workers, each collects $T$ steps of experience $(s_t, a_t, r_t, s_{t+1})$. Compute advantages $\hat{A}_t = \sum_{l=0}^{k-1}\gamma^l r_{t+l} + \gamma^k V(s_{t+k}) - V(s_t)$ for each transition. Compute the policy gradient loss $-\frac{1}{nT}\sum \log\pi(a_t|s_t)\hat{A}_t$ and the value loss $\frac{1}{nT}\sum (V(s_t) - R_t)^2$. Update shared network jointly.

> [!warning] Common Misconception
> A2C is sometimes called "the synchronous version of A3C," but it is worth noting that A2C came *after* A3C conceptually. In practice, A2C often outperforms A3C due to more stable gradient estimates from synchronised batch updates.

## Significance

A2C is a practical, GPU-scalable on-policy algorithm used widely in deep RL. It is implemented in Stable Baselines3 and serves as a robust baseline for comparing policy gradient approaches. Its synchronous design makes it easier to reason about and reproduce than A3C.
