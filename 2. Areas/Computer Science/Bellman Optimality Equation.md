**Tags:** #concept #rl
**Related:** [[Bellman Equation]], [[State Value Function]], [[Action Value Function]], [[Value Iteration]]

## Definition

The Bellman optimality equations define the value functions of the **optimal policy** $\pi_*$:

$$v_*(s) = \max_a \sum_{s',r} p(s',r|s,a)\left[r + \gamma\, v_*(s')\right]$$

$$q_*(s,a) = \sum_{s',r} p(s',r|s,a)\left[r + \gamma \max_{a'} q_*(s',a')\right]$$

> [!info] Key Intuition
> Whereas the Bellman equation averages over a fixed policy ($\sum_a \pi(a|s)$), the optimality equation takes a **max** — the optimal agent always picks the best action at each state.

## Relationship Between $v_*$ and $q_*$

$$v_*(s) = \max_a q_*(s,a) = \max_a \mathbb{E}\left[R_{t+1} + \gamma v_*(S_{t+1}) \mid S_t=s, A_t=a\right]$$

$$q_*(s,a) = \mathbb{E}\left[R_{t+1} + \gamma \max_{a'} q_*(S_{t+1},a') \mid S_t=s, A_t=a\right]$$

The $\max$ over $a'$ in the $q_*$ equation is what makes Q-learning off-policy: it targets the greedy value regardless of the behaviour policy.

## Optimal Policy Recovery

Once $q_*$ is known: $\pi_*(s) = \arg\max_a q_*(s,a)$ (model-free)

Once $v_*$ is known: $\pi_*(s) = \arg\max_a \sum_{s',r} p(s',r|s,a)[r + \gamma v_*(s')]$ (requires model)

## Computational Intractability

For most real problems (e.g. Backgammon: $\sim 10^{20}$ states, Chess: $\sim 10^{43}$), solving the optimality equations exactly is intractable. RL provides practical approximations.

> [!warning] Common Misconception
> The Bellman optimality equations are **nonlinear** (due to the max operator), unlike the linear Bellman equations for a fixed policy. They cannot be solved by matrix inversion — they require iterative methods (Value Iteration, Q-learning) or approximation.

## Significance

The Bellman optimality equations are the theoretical target of all RL algorithms. Value Iteration solves them directly (for small MDPs); Q-learning and DQN approximate $q_*$ from sampled experience.
