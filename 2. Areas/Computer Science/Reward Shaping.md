**Tags:** #concept #rl
**Related:** [[RL Frameworks]], [[Reinforcement Learning]], [[Reward Hypothesis]], [[Custom Environment Design]], [[Markov Decision Process]]

## Definition

Reward shaping is the practice of augmenting or modifying the reward signal provided by an environment to guide the agent toward desired behaviour more efficiently, without changing the optimal policy of the underlying task.

> [!info] Key Intuition
> The true reward signal is often sparse or delayed — reward shaping adds intermediate "hints" that tell the agent it is on the right track, dramatically speeding up learning without (when done correctly) distorting what the agent ultimately optimises.

## How It Works

Given an original reward function $r(s, a, s')$, shaped reward $r'$ adds a potential-based bonus:

$$r'(s, a, s') = r(s, a, s') + \gamma \Phi(s') - \Phi(s)$$

where $\Phi: \mathcal{S} \to \mathbb{R}$ is a potential function. Ng, Harada & Russell (1999) proved that this transformation is **policy-invariant**: the optimal policy under $r'$ is identical to the optimal policy under $r$.

## Practical Patterns

| Pattern | Description | Risk |
|---|---|---|
| **Potential-based shaping** | Bonus proportional to $\gamma \Phi(s') - \Phi(s)$ | Safe if $\Phi$ is well-designed |
| **Dense proxy reward** | Replace sparse terminal reward with step-level progress signals | Can distort the optimal policy if not potential-based |
| **Reward clipping** | Clip rewards to $[-1, +1]$ to stabilise training | Loses magnitude information |
| **Reward normalisation** | Scale rewards to unit variance online | Can mask domain signal |

## When to Use

- Environments with sparse terminal rewards (e.g. "reach the goal" with no intermediate signal)
- Tasks with very long episodes where the agent rarely sees positive reward early in training
- When curriculum learning is unavailable and the task is too hard to learn from scratch

> [!example]- Sparse vs Shaped Reward in Navigation
> **Sparse**: reward $= +1$ only when the agent reaches the goal; $0$ otherwise.
> **Shaped**: reward $= +1$ at goal, plus $\Phi(s) = -\text{distance\_to\_goal}(s)$, giving $r' = r + \gamma(-d') - (-d) = r + d - \gamma d'$. The agent receives a small positive signal whenever it moves closer.

> [!warning] Common Misconception
> Arbitrary reward bonuses (not potential-based) **can** change the optimal policy — the agent may learn to exploit the shaped reward rather than solve the actual task. Always verify that your shaping function satisfies the potential-based form, or validate the final policy against the original reward.

## Significance

Reward shaping is one of the most impactful levers in practical RL engineering. When designing a [[Custom Environment Design]], defining a well-shaped reward function is often more important than the choice of algorithm.

## From RL Applications

The **Cobra Effect** names the core failure mode: "you get what you incentivise, not what you intend." The name comes from British India, where a bounty on cobras led locals to breed cobras to collect the bounty — the incentive produced the opposite of the intended outcome.

**Reward polarity** also changes agent behaviour in a non-obvious way:
- **Positive rewards** encourage the agent to stay alive and accumulate more reward — useful when survival itself is a goal.
- **Negative rewards** encourage the agent to reach a terminal state quickly to stop the penalty — useful when finishing fast matters, but dangerous if the agent discovers that dying is the fastest terminal state.

**Staged rewards in time** sequence reward signals across task phases: early rewards guide exploration, later rewards enforce correctness. This is the intersection of reward shaping and [[Curriculum Learning]].
