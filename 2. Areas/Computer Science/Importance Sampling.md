**Tags:** #concept #rl
**Related:** [[Off-Policy MC Control]], [[Monte Carlo Methods]], [[Monte Carlo Prediction]], [[Exploration-Exploitation Tradeoff]]

## Definition

Importance Sampling is a general statistical technique for estimating expected values under one probability distribution (the **target** distribution $\pi$) given samples drawn from a different distribution (the **behavior** distribution $b$). In off-policy RL, it is used to re-weight observed returns so that they carry the correct expectation for the target policy.

> [!info] Key Intuition
> Returns sampled under behavior policy $b$ have the wrong expectation for target policy $\pi$. Multiplying each return by the ratio of how likely $\pi$ would have generated that trajectory versus how likely $b$ did — the importance sampling ratio — corrects the expectation.

## Importance Sampling Ratio

Given starting state $S_t$, the probability of the subsequent trajectory $A_t, S_{t+1}, A_{t+1}, \ldots, S_T$ under policy $\pi$ is:

$$\Pr\{A_t, S_{t+1}, \ldots, S_T \mid S_t,\, A_{t:T-1} \sim \pi\} = \prod_{k=t}^{T-1} \pi(A_k|S_k)\, p(S_{k+1}|S_k, A_k)$$

The importance sampling ratio cancels the unknown transition probabilities $p$ (they appear identically in numerator and denominator), leaving only policy probabilities:

$$\rho_{t:T-1} \doteq \frac{\prod_{k=t}^{T-1} \pi(A_k|S_k)}{\prod_{k=t}^{T-1} b(A_k|S_k)} = \prod_{k=t}^{T-1} \frac{\pi(A_k|S_k)}{b(A_k|S_k)}$$

Key property: if $\pi(a|s) > b(a|s)$ then $\rho > 1$ (upweight); if $\pi(a|s) < b(a|s)$ then $\rho < 1$ (downweight).

The corrected expectation: $\mathbb{E}[\rho_{t:T-1}\, G_t \mid S_t = s] = v_\pi(s)$

## Ordinary vs Weighted Importance Sampling

Let $\mathcal{T}(s)$ be the set of all time steps at which state $s$ is visited.

**Ordinary IS** (simple average of scaled returns):

$$V(s) \doteq \frac{\sum_{t \in \mathcal{T}(s)} \rho_{t:T(t)-1}\, G_t}{|\mathcal{T}(s)|}$$

**Weighted IS** (weighted average):

$$V(s) \doteq \frac{\sum_{t \in \mathcal{T}(s)} \rho_{t:T(t)-1}\, G_t}{\sum_{t \in \mathcal{T}(s)} \rho_{t:T(t)-1}}$$

| | Ordinary IS | Weighted IS |
|---|---|---|
| Bias | Unbiased | Biased (but consistent) |
| Variance | Unbounded (possibly infinite) | Finite variance |
| Practical preference | Rarely used | Preferred in practice |

In the blackjack off-policy estimation experiment, weighted IS produces substantially lower mean-squared error than ordinary IS across all episode counts.

## Incremental Update for Weighted IS

Maintaining the weighted average incrementally requires a cumulative weight sum $C_n$:

$$V_{n+1} \doteq V_n + \frac{W_n}{C_n}\left[G_n - V_n\right], \qquad C_{n+1} \doteq C_n + W_{n+1}$$

where $W_n$ is the importance sampling weight for the $n$-th return.

> [!example]- Off-Policy MC Prediction Algorithm Sketch
> Input: target policy $\pi$. Initialize $Q(s,a)$, $C(s,a) \leftarrow 0$.
> Each episode: use any behavior policy $b$ with coverage of $\pi$. Traverse episode backward, accumulating $G$ and importance weight $W \leftarrow W \cdot \pi(A_t|S_t)/b(A_t|S_t)$. Update $Q$ using the weighted incremental formula. If $W = 0$, break (trajectory diverged from $\pi$).

> [!warning] Common Misconception
> The importance sampling ratio does **not** require knowing the transition probabilities $p(s'|s,a)$ of the MDP — they cancel out algebraically. The ratio depends only on the two policies and the observed action sequence, making off-policy MC truly model-free.

## Significance

Importance Sampling is the core mechanism enabling off-policy learning. It is used in off-policy MC control, off-policy TD methods, and modern deep RL algorithms. Weighted IS is preferred universally in practice due to its finite variance guarantee.
