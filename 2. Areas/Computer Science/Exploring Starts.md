**Tags:** #concept #rl
**Related:** [[Monte Carlo Control]], [[Monte Carlo Methods]], [[On-Policy MC Control]], [[Exploration-Exploitation Tradeoff]]

## Definition

Exploring Starts (ES) is an assumption used in Monte Carlo control that requires every state-action pair $(s, a)$ to have a nonzero probability of being selected as the starting state-action pair of an episode. This guarantees that all pairs are visited infinitely often in the limit, enabling accurate estimation of $q_\pi$ for all pairs.

> [!info] Key Intuition
> If a deterministic policy never tries certain actions in certain states, those $Q(s,a)$ values never get updated — the agent can never discover whether those actions are better. Exploring Starts solves this by forcing random episode starts across all pairs.

## The Problem It Solves

When estimating action-values for a deterministic policy $\pi$, only one action per state is ever taken. The returns for all other actions from that state are never observed and $Q(s,a)$ cannot improve for the unchosen actions. Since the goal of policy evaluation for action values is to support policy improvement — which requires comparing all actions — this is a critical failure.

## MC ES Algorithm

```
Initialize: π(s) ∈ A(s) arbitrarily for all s
            Q(s,a) ∈ ℝ arbitrarily for all s,a
            Returns(s,a) ← empty list for all s,a

Loop forever (each episode):
  Choose S₀ ∈ S, A₀ ∈ A(S₀) randomly; all pairs have probability > 0
  Generate episode from S₀, A₀ following π
  G ← 0
  Loop for t = T-1, T-2, ..., 0:
    G ← γG + R_{t+1}
    Unless (S_t, A_t) appears in (S₀,A₀), ..., (S_{t-1},A_{t-1}):
      Append G to Returns(S_t, A_t)
      Q(S_t, A_t) ← average(Returns(S_t, A_t))
      π(S_t) ← argmax_a Q(S_t, a)
```

The key property: Monte Carlo ES **cannot converge to any suboptimal policy**, because all returns for each state-action pair are accumulated and averaged irrespective of the policy that was in force at the time of observation.

> [!example]- Blackjack Application
> In blackjack MC ES, at the start of each simulated game, a random player sum (12–21), dealer card (A–10), and first action (hit/stick) are selected uniformly. This ensures that even rarely-occurring game states are covered. After many episodes, the optimal policy shown is: stick when sum $\geq 20$, hit otherwise (with nuances for usable ace).

> [!warning] Common Misconception
> Exploring Starts is only practical in simulated environments where episode starts can be engineered. In real-world interaction, episode starting states are determined by the environment, not the agent — making ES inapplicable. The practical alternatives are $\varepsilon$-soft policies (on-policy) or Importance Sampling (off-policy).

## Significance

Exploring Starts is the simplest theoretical solution to the exploration problem in MC control. Its main value is pedagogical: it cleanly separates the exploration problem from the algorithm structure. Its limitation motivates the two practical approaches — on-policy and off-policy MC control.
