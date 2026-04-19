**Tags:** #concept #rl
**Related:** [[Monte Carlo Methods]], [[First-Visit vs Every-Visit MC]], [[State Value Function]], [[Policy Evaluation]]

## Definition

Monte Carlo Prediction estimates the state-value function $v_\pi(s)$ for a given policy $\pi$ by averaging the actual returns observed after visiting state $s$ across many episodes, without requiring a model of the environment.

> [!info] Key Intuition
> Since $v_\pi(s) = \mathbb{E}_\pi[G_t \mid S_t = s]$, the sample mean of observed returns is an unbiased estimator of $v_\pi(s)$ — and by the law of large numbers, it converges as the number of visits grows.

## How It Works

Generate episodes by following policy $\pi$: $S_0, A_0, R_1, S_1, A_1, R_2, \ldots, S_{T-1}, A_{T-1}, R_T$

For each time step $t$ in the episode, compute the return from that point forward:

$$G_t \doteq R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} + \cdots + \gamma^{T-t-1} R_T$$

Then average these returns over multiple trajectories to estimate $v_\pi(s)$.

**MC methods do not bootstrap**: the update target $G_t$ is an actual sampled return, not an estimate built from other value estimates. This contrasts with Dynamic Programming's Bellman backup:

$$v_{k+1}(s) = \sum_a \pi(a|s) \sum_{s',r} p(s',r|s,a)\left[r + \gamma v_k(s')\right]$$

The DP update requires $p(s',r|s,a)$; the MC update does not.

Both first-visit and every-visit MC converge to $v_\pi(s)$ as the number of visits (or first-visits) to $s$ goes to infinity.

> [!example]- Worked Example — Blackjack
> Policy: stick if player sum $\geq 20$, otherwise hit. Simulate 500,000 blackjack games following this policy. For each game, record the terminal reward (+1 win, -1 loss, 0 draw) as the return for every state visited. Average these returns per state to obtain $V(s) \approx v_\pi(s)$. After 500,000 episodes the value surface is well approximated.

> [!warning] Common Misconception
> MC prediction requires complete episodes — it cannot be applied to continuing (non-episodic) tasks directly. It is also strictly slower to update than TD methods, which can learn after every single step.

## Significance

MC prediction is the foundation for model-free policy evaluation. It is preferred when an environment model is unavailable and when complete episodes are tractable to generate. It is also less harmed by violations of the Markov property than bootstrapping methods, because it does not propagate value estimates through other value estimates.
