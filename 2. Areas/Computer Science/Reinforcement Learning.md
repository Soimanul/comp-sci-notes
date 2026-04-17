**Tags:** #concept #rl
**Related:** [[Introduction to Reinforcement Learning]], [[Exploration-Exploitation Tradeoff]], [[RL Policy]]

## Definition

A computational framework for learning goal-directed behaviour through interaction. An agent observes the state of an environment, selects actions, and receives scalar reward signals — learning to maximise cumulative reward without being told what the correct action is.

> [!info] Key Intuition
> RL is the only ML paradigm where the learner must discover good actions by trying them, not by being shown correct examples.

## The Agent-Environment Loop

At each discrete time step $t$:
1. Agent observes state $S_t \in \mathcal{S}$
2. Agent selects action $A_t \in \mathcal{A}(s)$ according to policy $\pi$
3. Environment transitions to $S_{t+1}$ and emits reward $R_{t+1}$

The trajectory is $S_0, A_0, R_1, S_1, A_1, R_2, \ldots$

## What Distinguishes RL from Other ML

| | Supervised | Unsupervised | Reinforcement |
|---|---|---|---|
| Feedback | Instructive (correct label) | None | Evaluative (scalar reward) |
| Training signal | Per-example | — | Delayed, sparse |
| Learns | Input→Output mapping | Structure | Behaviour policy |

**Evaluative feedback**: tells how good the action taken was — not which action would have been best. This is what creates the [[Exploration-Exploitation Tradeoff]].

## The Four Elements

1. **[[RL Policy]]** $\pi$: mapping from states to (distributions over) actions
2. **Reward signal** $R_t$: immediate scalar feedback from environment
3. **[[State Value Function]]** $v_\pi(s)$: expected cumulative reward from state $s$
4. **Model** (optional): agent's internal representation of environment dynamics

> [!example]- Worked Example
> A chess-playing agent: state = board position, action = legal move, reward = +1 win / -1 loss / 0 otherwise. The agent receives no reward for 50 moves, then gets +1. It must learn which moves were responsible for winning.

> [!warning] Common Misconception
> RL does not require a model of the environment. Model-free methods (TD learning, Q-learning) learn directly from experience; model-based methods use an explicit model of $p(s',r|s,a)$.

## Significance

RL provides the theoretical foundation for all goal-directed learning from experience: bandits, MDPs, TD methods, and deep RL (DQN, PPO, AlphaGo) are all specialisations of this framework.
