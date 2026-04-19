**Tags:** #concept #rl
**Related:** [[Temporal Difference Learning]], [[Temporal Differences]], [[SARSA]], [[Q-Learning]], [[Eligibility Traces]], [[TD(λ)]], [[Approximation Methods]]

## Definition

N-step TD methods generalise one-step TD (TD(0)) and Monte Carlo by bootstrapping after $n$ real steps rather than one or an entire episode. They form a continuous spectrum: $n=1$ is TD(0), $n=\infty$ is Monte Carlo.

> [!info] Key Intuition
> Instead of updating from the very next state (one-step TD) or waiting until the end of an episode (Monte Carlo), n-step TD looks ahead $n$ steps then bootstraps — the best methods often live at an intermediate $n$.

## N-Step Return

The Monte Carlo target uses the full return $G_t = R_{t+1} + \gamma R_{t+2} + \cdots + \gamma^{T-t-1} R_T$.

The one-step return is $G_{t:t+1} = R_{t+1} + \gamma V_t(S_{t+1})$.

The general **n-step return** is:

$$G_{t:t+n} \doteq R_{t+1} + \gamma R_{t+2} + \cdots + \gamma^{n-1} R_{t+n} + \gamma^n V_{t+n-1}(S_{t+n})$$

All n-step returns are approximations to the full return $G_t$; they differ only in where bootstrapping begins.

## N-Step TD Prediction Update

$$V_{t+n}(S_t) \doteq V_{t+n-1}(S_t) + \alpha\left[G_{t:t+n} - V_{t+n-1}(S_t)\right], \quad 0 \le t < T$$

The update for state $S_t$ is made $n$ steps later, once $G_{t:t+n}$ is known.

## N-Step SARSA

For control, replace state values with action values. The n-step SARSA return is:

$$G_{t:t+n} = Q_{t-1}(S_t, A_t) + \sum_{k=t}^{\min(t+n, T)-1} \gamma^{k-t}\left[R_{k+1} + \gamma Q_k(S_{k+1}, A_{k+1}) - Q_{k-1}(S_k, A_k)\right]$$

The agent uses $\varepsilon$-greedy to act and updates $Q(S_\tau, A_\tau)$ at time $\tau = t - n + 1$.

## N-Step Off-Policy Learning

For off-policy n-step TD, correct for the discrepancy between target policy $\pi$ and behaviour policy $b$ using an **importance sampling ratio**:

$$\rho_{t:h} \doteq \prod_{k=t}^{\min(h, T-1)} \frac{\pi(A_k | S_k)}{b(A_k | S_k)}$$

The update becomes:

$$V_{t+n}(S_t) \doteq V_{t+n-1}(S_t) + \alpha\, \rho_{t:t+n-1}\left[G_{t:t+n} - V_{t+n-1}(S_t)\right]$$

> [!example]- Worked Example
> 19-state random walk: uniform random policy on a chain of 19 states. Empirically, $n=4$ or $n=8$ minimises RMS error at a given learning rate, outperforming both $n=1$ (TD(0)) and $n=\infty$ (MC). The optimal $n$ grows with the complexity of the task.

> [!warning] Common Misconception
> N-step methods require waiting $n$ steps before updating, introducing a delay. This does NOT mean they are less online than TD(0) — they still update incrementally, just with a $n$-step lag. The extra memory required (storing $n$ transitions) is the real practical cost.

## Significance

N-step methods free the algorithm from the "tyranny of the single time step." They are the conceptual bridge to eligibility traces (TD($\lambda$), Chapter 12), which efficiently implement infinite superpositions of n-step returns using a single trace variable.
