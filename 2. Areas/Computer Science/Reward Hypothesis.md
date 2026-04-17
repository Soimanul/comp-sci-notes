**Tags:** #concept #rl
**Related:** [[Reinforcement Learning]], [[Discounted Return]], [[State Value Function]]

## Definition

The Reward Hypothesis states that all goals and purposes of an agent can be well thought of as the maximisation of the expected value of the cumulative sum of a scalar signal (the reward).

> [!info] Key Intuition
> Every goal — from winning chess to walking to generating coherent text — can be encoded as a single number to maximise. The art of RL is designing a reward function that correctly captures the intended goal.

## Formal Statement

The agent's objective is to maximise:
$$G_t = R_{t+1} + \gamma R_{t+2} + \gamma^2 R_{t+3} + \cdots = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}$$

where $\gamma \in [0,1]$ is the discount factor.

## Implications

- The reward signal is the **only** channel through which the environment communicates what matters
- Poorly specified rewards lead to misaligned behaviour (**reward hacking**)
- The hypothesis is a modelling choice, not an empirical truth — it is powerful but not uncontested

> [!warning] Common Misconception
> The reward signal encodes **what** you want, not **how** to achieve it. Do not reward subgoals directly unless you are certain they are aligned with the ultimate objective — the agent will optimise exactly what you specify.

## Significance

The Reward Hypothesis is the foundational commitment of RL: it justifies why a scalar feedback signal is sufficient to learn arbitrarily complex behaviour.
