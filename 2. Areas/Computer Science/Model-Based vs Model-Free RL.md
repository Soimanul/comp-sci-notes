**Tags:** #concept #rl
**Related:** [[Reinforcement Learning]], [[Policy Evaluation]], [[Q-Learning]], [[Dynamic Programming for RL]]

## Definition

A distinction in how RL algorithms use knowledge of the environment's dynamics:

- **Model-based RL**: the agent has or learns a model $p(s',r|s,a)$ and uses it to plan (compute value functions without additional interaction)
- **Model-free RL**: the agent learns value functions or policies directly from sampled experience, without modelling the dynamics

> [!info] Key Intuition
> Model-based = know the rules, then plan. Model-free = learn only from playing the game.

## The Backup Diagram Perspective

In the backup diagram for $v_\pi(s)$:
- **Model-based** (DP): requires knowing $p(s',r|s,a)$ for all branches — a **full backup**
- **Model-free** (MC, TD): samples a single trajectory branch — a **sample backup**

## Comparison

| | Model-Based | Model-Free |
|---|---|---|
| Data requirement | Needs $p(s',r|s,a)$ | Needs sampled experience |
| Planning | Possible (DP, value iteration) | Not possible directly |
| Examples | Dynamic Programming | Q-learning, SARSA, Monte Carlo |
| Sample efficiency | High | Lower |
| Generalises to unknown environments | No | Yes |

## POMDP Case

In a Partially Observable MDP (POMDP), the agent does not observe $s$ directly — it observes $o_t$ generated from hidden state $x_t$ via emission probabilities $P(o|x)$. The agent must maintain a **belief state** $b(x)$ — a probability distribution over hidden states.

POMDPs are significantly harder: the effective state space is the space of belief distributions (continuous even if $\mathcal{X}$ is finite).

> [!warning] Common Misconception
> Dynamic Programming is not a "learning" algorithm — it requires a complete model and performs planning, not learning from interaction. RL algorithms that learn from experience are either MC or TD-based.

## Significance

This distinction determines which algorithms are applicable. Real-world environments rarely provide perfect dynamics, making model-free methods dominant in practice.
