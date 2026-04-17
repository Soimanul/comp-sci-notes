**Tags:** #concept #rl
**Related:** [[Policy Evaluation]], [[Policy Iteration]], [[Generalized Policy Iteration]], [[Action Value Function]]

## Definition

The Policy Improvement Theorem states: if policy $\pi'$ is defined by acting greedily with respect to $v_\pi$ (the value function of $\pi$), then $\pi'$ is at least as good as $\pi$:

$$v_{\pi'}(s) \geq v_\pi(s) \quad \forall s \in \mathcal{S}$$

> [!info] Key Intuition
> If you can find even one state where a different action gives a higher expected value, and you always take that action there, the new policy is strictly better. Applying this greedy improvement everywhere guarantees improvement.

## Formal Statement

Given $v_\pi$, define the greedy improvement:
$$\pi'(s) = \arg\max_a q_\pi(s,a) = \arg\max_a \sum_{s',r} p(s',r|s,a)\left[r + \gamma\, v_\pi(s')\right]$$

**Theorem**: if $q_\pi(s, \pi'(s)) \geq v_\pi(s)$ for all $s$, then $v_{\pi'}(s) \geq v_\pi(s)$ for all $s$.

**Proof sketch** (telescoping):
$$v_\pi(s) \leq q_\pi(s,\pi'(s)) = \mathbb{E}[R_{t+1} + \gamma v_\pi(S_{t+1}) \mid S_t=s, A_t=\pi'(s)]$$
$$\leq \mathbb{E}[R_{t+1} + \gamma q_\pi(S_{t+1}, \pi'(S_{t+1})) \mid \ldots] \leq \cdots \leq v_{\pi'}(s)$$

## When Improvement Stops

If $\pi' = \pi$ (no state improves by switching), then $v_\pi = v_*$ — we have found the optimal policy.

> [!warning] Common Misconception
> Policy improvement does not require re-evaluating $v_{\pi'}$ from scratch before the next improvement step. Truncated evaluation (as in Value Iteration, or online TD updates) still guarantees eventual convergence due to GPI.

## Significance

The Policy Improvement Theorem guarantees that greedy improvement always makes progress, providing the theoretical justification for the entire DP/RL optimisation cycle.
