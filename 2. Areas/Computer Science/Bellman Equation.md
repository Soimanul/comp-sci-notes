**Tags:** #concept #rl
**Related:** [[State Value Function]], [[Action Value Function]], [[Markov Decision Process]], [[Bellman Optimality Equation]]

## Definition

The Bellman equation for a policy $\pi$ expresses the value of a state recursively in terms of the values of its successor states:

$$v_\pi(s) = \sum_a \pi(a|s) \sum_{s',r} p(s',r|s,a)\left[r + \gamma\, v_\pi(s')\right]$$

> [!info] Key Intuition
> The value of where you are equals the expected immediate reward plus the discounted expected value of where you end up. This recursive consistency condition uniquely defines $v_\pi$.

## Derivation

Starting from the definition:
$$v_\pi(s) = \mathbb{E}_\pi[G_t \mid S_t = s] = \mathbb{E}_\pi[R_{t+1} + \gamma G_{t+1} \mid S_t = s]$$
$$= \sum_a \pi(a|s) \sum_{s',r} p(s',r|s,a)\left[r + \gamma\, \mathbb{E}_\pi[G_{t+1} \mid S_{t+1}=s']\right]$$
$$= \sum_a \pi(a|s) \sum_{s',r} p(s',r|s,a)\left[r + \gamma\, v_\pi(s')\right]$$

## Bellman Equation for $q_\pi$

$$q_\pi(s,a) = \sum_{s',r} p(s',r|s,a)\left[r + \gamma \sum_{a'} \pi(a'|s')\, q_\pi(s',a')\right]$$

## Backup Diagram

The backup diagram for $v_\pi$:
- Open circle = state node
- Filled circle = action node
- Branches = stochastic transitions weighted by $\pi(a|s)$ and $p(s',r|s,a)$

Value information flows **back** from successor states to the current state — hence "backup."

> [!example]- Worked Example
> 2-state MDP, $\pi$ = always go right, $\gamma=0.9$, reward = 0 for left state, +1 for right: $v_\pi(\text{right}) = 1 + 0.9 v_\pi(\text{right}) \Rightarrow v_\pi = 10$. $v_\pi(\text{left}) = 0 + 0.9 \times 10 = 9$.

> [!warning] Common Misconception
> The Bellman equation is not an algorithm — it is a system of $|\mathcal{S}|$ linear equations in $|\mathcal{S}|$ unknowns. It can be solved directly (matrix inversion) or iteratively (policy evaluation). The iterative version is the practical algorithm.

## Significance

The Bellman equation is the central mathematical object of RL. Every algorithm (DP, TD, MC) is either solving, approximating, or sampling from the Bellman equation.
