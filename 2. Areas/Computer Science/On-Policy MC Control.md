**Tags:** #concept #rl
**Related:** [[Monte Carlo Control]], [[Monte Carlo Methods]], [[Exploring Starts]], [[Off-Policy MC Control]], [[Epsilon-Greedy Action Selection]], [[Exploration-Exploitation Tradeoff]]

## Definition

On-Policy MC Control is a Monte Carlo control method that evaluates and improves the same policy used to generate episodes. To maintain continual exploration without Exploring Starts, the policy is kept **$\varepsilon$-soft**: every action in every state has probability at least $\varepsilon / |\mathcal{A}(s)|$ of being selected, while the greedy action gets the remaining probability mass.

> [!info] Key Intuition
> On-policy methods commit to always exploring — the price paid is that they converge to the best policy *among $\varepsilon$-soft policies*, not the globally optimal deterministic policy. But no unrealistic assumption about episode starts is needed.

## $\varepsilon$-Soft Policy Structure

For the greedy action $A^* = \arg\max_a Q(S_t, a)$:

$$\pi(a \mid S_t) \leftarrow \begin{cases} 1 - \varepsilon + \varepsilon/|\mathcal{A}(S_t)| & \text{if } a = A^* \\ \varepsilon / |\mathcal{A}(S_t)| & \text{if } a \neq A^* \end{cases}$$

This ensures $\pi(a|s) > 0$ for all $a$, guaranteeing all state-action pairs are visited infinitely often.

## Algorithm — On-Policy First-Visit MC Control

```
Algorithm parameter: small ε > 0
Initialize: π ← arbitrary ε-soft policy
            Q(s,a) ∈ ℝ arbitrarily for all s,a
            Returns(s,a) ← empty list for all s,a

Repeat forever (each episode):
  Generate episode following π: S₀,A₀,R₁,...,S_{T-1},A_{T-1},R_T
  G ← 0
  Loop for t = T-1, T-2, ..., 0:
    G ← γG + R_{t+1}
    Unless (S_t,A_t) appears earlier in episode:
      Append G to Returns(S_t, A_t)
      Q(S_t, A_t) ← average(Returns(S_t, A_t))
      A* ← argmax_a Q(S_t, a)   (ties broken arbitrarily)
      For all a ∈ A(S_t):
        π(a|S_t) ← (1-ε + ε/|A(S_t)|) if a = A*, else ε/|A(S_t)|
```

## Guarantee

Any $\varepsilon$-greedy policy with respect to $q_\pi$ is an improvement over any $\varepsilon$-soft policy $\pi$, as assured by the **Policy Improvement Theorem**. The method converges to the optimal policy within the class of $\varepsilon$-soft policies.

The tradeoff: exploring starts is eliminated, but the agent can only reach the optimal $\varepsilon$-soft policy — a near-optimal policy that still explores with probability $\varepsilon$ forever.

> [!example]- Contrast with MC ES
> MC ES (Exploring Starts) can reach a fully deterministic optimal policy because it guarantees exploration through the episode start distribution, not through a stochastic policy. On-policy MC gives up the deterministic optimum but removes the need to control episode starts.

> [!warning] Common Misconception
> On-policy MC does not converge to a suboptimal policy in a harmful sense — the $\varepsilon$-soft optimal policy is very close to the true optimal policy when $\varepsilon$ is small. The residual suboptimality is bounded and diminishes as $\varepsilon \to 0$.

## Significance

On-policy MC control is the standard practical approach when interaction is direct (real environment, not simulation). It motivates the use of $\varepsilon$-greedy exploration in nearly all tabular RL algorithms, including SARSA.
