**Tags:** #concept #rl
**Related:** [[Actor-Critic]], [[Actor-Critic Methods]], [[State Value Function]], [[Action Value Function]], [[Generalized Advantage Estimation]], [[Baseline in Policy Gradients]]

## Definition

The advantage function $A^\pi(s, a)$ measures how much better action $a$ is in state $s$ compared to the average action under policy $\pi$:

$$A^\pi(s, a) = Q^\pi(s, a) - V^\pi(s)$$

where $Q^\pi(s, a)$ is the action-value (expected return from taking $a$ in $s$ then following $\pi$) and $V^\pi(s) = \sum_a \pi(a|s) Q^\pi(s,a)$ is the state value (expected return from $s$ under $\pi$).

> [!info] Key Intuition
> The advantage answers "how much better is this specific action compared to what I would usually do here?" — it is a centred version of Q that automatically zeroes out the state-level baseline.

## Why Use the Advantage

In the policy gradient update:

$$\nabla J(\theta) \propto \mathbb{E}_\pi\!\left[Q^\pi(S_t, A_t)\,\nabla\ln\pi(A_t|S_t,\theta)\right]$$

Substituting $A^\pi$ for $Q^\pi$ is valid because $V^\pi(s)$ is a valid baseline (it does not depend on $a$), and it does not change the expected gradient. However, it reduces variance because the advantage signal is centred around zero, whereas the raw $Q$ may be uniformly large across all actions.

## Estimation in Practice

In actor-critic algorithms, $V^\pi(s)$ is approximated by the critic $\hat{v}(s, \mathbf{w})$. The advantage is estimated via the TD error:

$$\hat{A}(s, a) \approx \delta_t = R_{t+1} + \gamma\hat{v}(S_{t+1}, \mathbf{w}) - \hat{v}(S_t, \mathbf{w})$$

This one-step estimate is biased (because $\hat{v}$ is approximate) but has much lower variance than the full Monte Carlo estimate. For a richer estimate, see [[Generalized Advantage Estimation]].

From the A3C paper, using $V^\pi(s_t)$ as the baseline $b_t$:
$$A(s_t, a_t; \theta, \theta_v) = Q(s_t, a_t) - V(s_t) = R_t - b_t(s_t) \approx R_t - V(s_t; \theta_v)$$

where $R_t = \sum_{i=0}^{k-1}\gamma^i r_{t+i} + \gamma^k V(s_{t+k}; \theta_v)$ is the $k$-step return.

> [!example]- Advantage in CartPole
> Suppose $V^\pi(s) = 50$ (the agent typically accumulates 50 reward from state $s$). If action "push left" gives $Q = 60$, its advantage is $+10$; if "push right" gives $Q = 40$, its advantage is $-10$. The policy gradient reinforces "push left" and suppresses "push right", even though both Q values are large and positive.

> [!warning] Common Misconception
> The advantage function is *not* directly observable — it must be estimated. The common approximation $\hat{A}_t \approx \delta_t$ (the TD error) is a biased but low-variance estimate. Using the full Monte Carlo return minus a learned baseline is unbiased but high-variance.

## Significance

The advantage function is the central quantity in advantage actor-critic (A2C/A3C), PPO, and GAE. By working with advantages rather than raw returns or Q values, these algorithms achieve stable gradient estimates with naturally centred, zero-mean learning signals.
