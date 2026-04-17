**Tags:** #concept #rl
**Related:** [[Dynamic Programming for RL]], [[Value Iteration]], [[Policy Iteration]]

## Definition

Asynchronous DP algorithms update state values in any order — not necessarily sweeping through the full state space synchronously. Individual states can be updated once, many times, or in any sequence, as long as all states continue to be updated over time.

> [!info] Key Intuition
> Instead of sweeping every state once per iteration, update states opportunistically — e.g. prioritise states the agent currently visits, or states whose estimates changed most recently.

## Why Asynchronous DP Matters

Synchronous DP sweeps are $O(|\mathcal{S}| \cdot |\mathcal{A}|)$ per iteration. For large state spaces this is prohibitive. Asynchronous methods:
- Allow real-time interaction (update states as they are visited)
- Enable prioritised sweeping (update high-error states first)
- Are the basis for online RL (TD methods update one state per step)

## Variants

**In-place DP**: immediately use newly computed $V(s)$ when updating other states (no copy of $V_\text{old}$). Often converges faster than synchronous.

**Prioritised sweeping**: maintain a priority queue ordered by $|\mathcal{T}^* V(s) - V(s)|$ (Bellman error). Update high-priority states first — dramatically reduces sweeps needed.

**Real-time DP**: only update states on the agent's actual trajectory. States not visited are not updated. Converges only for relevant states.

> [!warning] Common Misconception
> Asynchronous DP still requires a complete model $p(s',r|s,a)$. It is not the same as model-free RL — it relaxes the **synchronous sweep** requirement, not the model requirement.

## Significance

Asynchronous DP bridges the gap between classic DP and TD learning: online TD methods are essentially asynchronous DP with sampled (instead of expected) backups. Prioritised experience replay in DQN is the deep RL equivalent of prioritised sweeping.
