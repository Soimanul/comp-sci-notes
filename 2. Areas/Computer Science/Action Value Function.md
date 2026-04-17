**Tags:** #concept #rl
**Related:** [[State Value Function]], [[Bellman Equation]], [[Q-Learning]], [[SARSA]]

## Definition

The action-value function $q_\pi(s,a)$ gives the expected return when starting in state $s$, taking action $a$, and thereafter following policy $\pi$:

$$q_\pi(s,a) = \mathbb{E}_\pi[G_t \mid S_t = s,\, A_t = a]$$

> [!info] Key Intuition
> $q_\pi(s,a)$ answers: "If I'm in state $s$, take action $a$ (possibly off-policy), then follow $\pi$ — how much total reward do I expect?" This makes it directly useful for policy improvement without needing the model.

## Relationship to $v_\pi$

$$v_\pi(s) = \sum_a \pi(a|s)\, q_\pi(s,a)$$

$$q_\pi(s,a) = \sum_{s',r} p(s',r|s,a)\left[r + \gamma\, v_\pi(s')\right]$$

## Optimal Action-Value Function

$$q_*(s,a) = \mathbb{E}\left[R_{t+1} + \gamma \max_{a'} q_*(S_{t+1},a') \mid S_t=s,\, A_t=a\right]$$

$$= \sum_{s',r} p(s',r|s,a)\left[r + \gamma \max_{a'} q_*(s',a')\right]$$

The optimal policy selects $\pi_*(s) = \arg\max_a q_*(s,a)$.

> [!example]- Worked Example
> Q-learning learns $q_*$ directly: after observing $(s, a, r, s')$, update:
> $Q(s,a) \leftarrow Q(s,a) + \alpha\left[r + \gamma \max_{a'} Q(s',a') - Q(s,a)\right]$

> [!warning] Common Misconception
> Knowing $q_*$ is more directly useful than knowing $v_*$ for a model-free agent: improving the policy from $q_*$ requires only $\arg\max_a q_*(s,a)$, while improving from $v_*$ requires knowing $p(s',r|s,a)$ to evaluate the one-step lookahead.

## Significance

Q-functions are the central object in model-free value-based RL (SARSA, Q-learning, DQN). The action-value formulation eliminates the need for an explicit model during policy improvement.
