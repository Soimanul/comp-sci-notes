**Tags:** #concept #rl
**Related:** [[Action Value Function]], [[Bellman Equation]], [[RL Policy]], [[Discounted Return]]

## Definition

The state-value function $v_\pi(s)$ gives the expected return when starting in state $s$ and following policy $\pi$ thereafter:

$$v_\pi(s) = \mathbb{E}_\pi[G_t \mid S_t = s]$$

> [!info] Key Intuition
> $v_\pi(s)$ answers: "If I'm in state $s$ and follow policy $\pi$ from here on, how much total reward can I expect?"

## Bellman Equation for $v_\pi$

Expanding the expectation one step gives the recursive Bellman equation:

$$v_\pi(s) = \sum_a \pi(a|s) \sum_{s',r} p(s',r|s,a)\left[r + \gamma\, v_\pi(s')\right]$$

This expresses the value of $s$ in terms of the values of its successor states — the foundation of dynamic programming and TD methods.

## Optimal State-Value Function

$$v_*(s) = \max_\pi v_\pi(s) = \max_a \sum_{s',r} p(s',r|s,a)\left[r + \gamma\, v_*(s')\right]$$

If $v_*$ is known, the optimal policy is the greedy policy w.r.t. $v_*$.

> [!example]- Worked Example
> In a 3-state chain (A → B → terminal) with $\gamma=0.9$ and reward +1 on reaching terminal: $v_\pi(\text{B}) = 0 + 0.9 \times 1 = 0.9$; $v_\pi(\text{A}) = 0 + 0.9 \times 0.9 = 0.81$.

> [!warning] Common Misconception
> $v_\pi(s)$ depends on the policy $\pi$. The same state can have very different values under different policies. Only $v_*(s)$ is policy-independent (it is the value under the optimal policy).

## Significance

State-value functions are the primary object computed in policy evaluation and the basis for policy improvement. All DP, MC, and TD algorithms either estimate or use $v_\pi$ (or $v_*$).
