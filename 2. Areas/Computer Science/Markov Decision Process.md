**Tags:** #concept #rl
**Related:** [[Markov Chain]], [[Graphs, Search, and MDPs]], [[Bellman Equation]], [[RL Policy]]

## Definition

A Markov Decision Process (MDP) is a mathematical framework for sequential decision-making under uncertainty. It extends a Markov chain by adding agent-controlled actions and reward signals.

A finite MDP is defined by $(\mathcal{S}, \mathcal{A}, p, \mathcal{R}, \gamma)$:
- $\mathcal{S}$: finite set of states
- $\mathcal{A}(s)$: finite set of actions available in state $s$
- $p(s',r \mid s,a)$: **dynamics function** — probability of transitioning to $s'$ and receiving reward $r$ when taking action $a$ in state $s$
- $\mathcal{R} \subset \mathbb{R}$: set of possible rewards
- $\gamma \in [0,1]$: discount factor

> [!info] Key Intuition
> An MDP is a Markov chain where you choose the transition probabilities at each step by selecting an action. The agent controls which edges in the state graph it traverses.

## The Dynamics Function

$$p(s',r \mid s,a) = \text{Pr}\{S_t=s', R_t=r \mid S_{t-1}=s, A_{t-1}=a\}$$

All other useful quantities derive from $p$:
- State-transition: $p(s' \mid s,a) = \sum_r p(s',r \mid s,a)$
- Expected reward: $r(s,a) = \sum_r r \sum_{s'} p(s',r \mid s,a)$

## Trajectory and Interaction

$$S_0, A_0, R_1, S_1, A_1, R_2, S_2, \ldots$$

The **structure of an MDP**: $s_0 \to \pi(a|s_0) \to A_0 \to T(s_1|s_0,A_0) \to S_1 \to \ldots$

## Episodic vs Continuing Tasks

- **Episodic**: trajectory ends at terminal state $s_T$ (e.g. game over); return is finite sum $G_t = \sum_{k=0}^{T-t-1} R_{t+k+1}$
- **Continuing**: no terminal state; return requires discounting $G_t = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}$
- **Unification**: make $s_T$ an absorbing state with $r=0$ and $\gamma=1$ for episodic tasks

> [!example]- Worked Example
> Recycling Robot: states = {high battery, low battery}, actions = {search, wait, recharge}. Dynamics: in state "high", action "search" transitions to "high" with prob 0.7 (reward +r_search) or "low" with 0.3 (reward +r_search). The dynamics function encodes all these probabilities.

> [!warning] Common Misconception
> The Markov property is on the **state**, not the agent's decision. A fully observable MDP satisfies the Markov property. A POMDP does not — the agent sees observations $o_t$ generated from a hidden state $x_t$, and the true state is not directly accessible.

## Significance

The MDP is the central formal model of RL. All algorithms — DP, TD, Monte Carlo, policy gradient — are methods for solving (exactly or approximately) the MDP optimisation problem.
