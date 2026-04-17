**Tags:** #concept #rl
**Related:** [[Markov Decision Process]], [[Reward Hypothesis]], [[State Value Function]]

## Definition

The **discounted return** $G_t$ is the sum of future rewards, geometrically weighted by discount factor $\gamma$:

$$G_t = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1} = R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} + \cdots$$

> [!info] Key Intuition
> A reward one step away is worth $\gamma$ of a reward now; two steps away is worth $\gamma^2$. Discounting makes the infinite-horizon sum finite and encodes a preference for immediate reward.

## The Recursive Identity

$$G_t = R_{t+1} + \gamma G_{t+1}$$

This single identity underlies all Bellman equations: the value of the current state equals the immediate reward plus the discounted value of the next state.

## Role of $\gamma$

| $\gamma$ | Effect |
|---|---|
| $\gamma = 0$ | Myopic: only immediate reward matters |
| $\gamma \to 1$ | Far-sighted: all future rewards equally weighted |
| $\gamma \in (0,1)$ | Geometric decay: recent rewards matter more |

For continuing tasks, $\gamma < 1$ is necessary to ensure $G_t < \infty$ (geometric series: $G_t \leq R_{\max}/(1-\gamma)$).

## Episodic Tasks

For episodic tasks ending at time $T$:
$$G_t = \sum_{k=0}^{T-t-1} R_{t+k+1}$$

Discounting is optional but may still be applied. Setting $\gamma = 1$ and having $T$ finite gives the undiscounted episodic return.

> [!warning] Common Misconception
> Discounting is not just a mathematical convenience — it also provides an economic interpretation (money now is worth more than future money) and avoids circular definitions in continuing tasks. However, for episodic tasks, the choice of $\gamma$ significantly affects what optimal behaviour looks like.

## Significance

The discounted return is the quantity all RL algorithms seek to maximise. Its recursive structure (via $G_t = R_{t+1} + \gamma G_{t+1}$) is what makes bootstrapping possible in TD methods.
