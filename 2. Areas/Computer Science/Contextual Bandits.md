**Tags:** #concept #rl
**Related:** [[k-Armed Bandit Problem]], [[Reinforcement Learning]], [[Exploration-Exploitation Tradeoff]]

## Definition

An extension of the k-armed bandit where the agent observes a **context** (state vector) before selecting an action. The optimal action can differ by context, so the agent must learn a policy $\pi: \text{context} \to \text{action}$ rather than a single best arm.

> [!info] Key Intuition
> Standard bandits ignore who you're serving. Contextual bandits personalise: showing the right ad to the right user at the right time, rather than the globally best ad to everyone.

## Hierarchy of Problems

| Problem | State influences action? | Action influences next state? |
|---|---|---|
| k-Armed Bandit | No | No |
| **Contextual Bandit** | **Yes** | **No** |
| Full RL (MDP) | Yes | Yes |

The contextual bandit sits between MABs and full RL: it requires learning a policy (like RL) but each action still only affects the immediate reward (like a bandit).

## Formal Definition

At each round $n$:
1. Agent observes context $x_n \in \mathcal{X}$
2. Selects action $a_n \in \{1,\ldots,k\}$
3. Receives reward $r_n = f(x_n, a_n) + \text{noise}$
4. Next context $x_{n+1}$ is drawn independently (actions do not affect context)

The context may encode user features, time of day, environmental state, etc.

## Applications

- News article recommendation (NYT uses contextual MABs)
- Online advertising (match ad to user profile)
- Clinical trials (personalised treatment selection)
- Search result ranking

> [!example]- Worked Example
> User context = (age=25, location=NYC, device=mobile). Standard bandit would show the same ad to this user as to everyone. Contextual bandit learns: for young urban mobile users, Ad 3 has 12% CTR vs 4% for Ad 1 — so it shows Ad 3 to this user specifically.

> [!warning] Common Misconception
> Contextual bandits are NOT full RL: the key distinction is that actions affect only immediate rewards, not future contexts. If your ad choice changes what articles the user reads next (affecting their future preferences), you have a full RL problem, not a contextual bandit.

## Significance

Contextual bandits bridge the gap between simple bandits and full RL. They are the dominant framework for real-time personalisation at scale (recommendation, ads, search).
