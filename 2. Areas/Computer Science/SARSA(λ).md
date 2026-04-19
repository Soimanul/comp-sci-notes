**Tags:** #concept #rl
**Related:** [[Eligibility Traces]], [[TD(λ)]], [[SARSA]], [[Approximation Methods]], [[Semi-Gradient TD]]

## Definition

SARSA(λ) is the extension of SARSA to eligibility traces. It applies the TD(λ) mechanism to *action-value* function approximation, producing an on-policy control algorithm that uses a trace vector over action-value features to efficiently implement multi-step credit assignment.

> [!info] Key Intuition
> SARSA(λ) is to SARSA what TD(λ) is to TD(0): the eligibility trace propagates the current TD error backward through the recent trajectory of (state, action) pairs, crediting all recently visited state-action pairs for the current outcome.

## Algorithm

The action-value trace is accumulated and decayed at each step:

$$\mathbf{z}_t \leftarrow \gamma\lambda\,\mathbf{z}_{t-1} + \nabla\hat{q}(S_t, A_t, \mathbf{w}_t)$$

The TD error for SARSA is:

$$\delta_t = R_{t+1} + \gamma\hat{q}(S_{t+1}, A_{t+1}, \mathbf{w}_t) - \hat{q}(S_t, A_t, \mathbf{w}_t)$$

Weight update at each step:

$$\mathbf{w}_{t+1} \leftarrow \mathbf{w}_t + \alpha\,\delta_t\,\mathbf{z}_t$$

Note that $A_{t+1}$ is chosen from the current policy $\pi$ (e.g. ε-greedy), maintaining on-policy correctness.

## Relationship to Watkins's Q(λ)

Watkins's Q(λ) extends Q-learning (off-policy) with eligibility traces by cutting the trace to zero after any non-greedy action. SARSA(λ) avoids this trace-cutting problem by remaining on-policy — the trace accumulates smoothly over the entire trajectory.

The Tree-Backup(λ) algorithm extends this idea further, achieving off-policy eligibility traces *without* importance sampling, by generalising Expected SARSA to arbitrary target policies with exponentially weighted multi-step backups.

> [!example]- Gridworld with SARSA(λ)
> In a gridworld with delayed rewards (goal only at episode end), SARSA(0) must propagate reward backward one step at a time over many episodes. SARSA(λ ≈ 0.9) propagates the terminal reward backward through the entire episode via the trace in a *single* episode, dramatically accelerating learning.

> [!warning] Common Misconception
> SARSA(λ) is on-policy, so the trace accumulates over the *actual* actions taken (including exploratory ones). This differs from Q(λ), which only accumulates the trace for greedy actions and cuts it after exploration — SARSA(λ) is therefore simpler to implement and avoids the trace-cutting heuristic.

## Significance

SARSA(λ) is the standard on-policy control algorithm with eligibility traces. Its efficient backward view makes it particularly effective in tasks with long episodes and delayed rewards, where credit must be assigned across many time steps. It extends naturally from tabular to linear function approximation.
