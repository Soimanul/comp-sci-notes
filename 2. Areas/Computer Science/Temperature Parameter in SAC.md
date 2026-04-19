**Tags:** #concept #rl
**Related:** [[Soft Actor-Critic (SAC)]], [[Maximum Entropy RL]], [[Entropy Regularization in RL]], [[Research Papers and Innovation Trends B]]

## Definition

The temperature parameter $\alpha$ in Soft Actor-Critic is a scalar hyperparameter that controls the relative weight given to the entropy of the policy versus the expected reward in the maximum entropy RL objective. A higher $\alpha$ encourages more exploration (higher-entropy policies); $\alpha = 0$ recovers standard RL.

> [!info] Key Intuition
> Temperature is the "dial" between full exploitation ($\alpha = 0$, greedy) and pure exploration ($\alpha \to \infty$, uniform random). Setting it correctly is critical because, unlike in standard RL where reward scaling is irrelevant, in maximum entropy RL the reward scale matters relative to the entropy scale.

## The Problem with Manual Temperature Tuning

In the original SAC (Haarnoja et al., 2018 v1), $\alpha$ is a fixed hyperparameter. This creates a fundamental difficulty:

- In standard RL, multiplying all rewards by a constant does not change the optimal policy.
- In maximum entropy RL, scaling the reward changes the optimal temperature: larger rewards require a larger $\alpha$ to keep the entropy term relevant.
- A suboptimal $\alpha$ drastically degrades performance — too high and the agent explores randomly; too low and it converges prematurely to a bad local optimum.

## Autotuned Temperature (SAC v2)

Haarnoja et al. (2018 v2, "SAC Algorithms and Applications") introduced an automatic temperature tuning method. Instead of fixing $\alpha$, the algorithm learns it by solving a constrained optimization:

$$\min_\alpha \; \mathbb{E}_{a \sim \pi}\!\left[-\alpha \log \pi(a|s) - \alpha \hat{H}\right]$$

where $\hat{H}$ is a target entropy (typically set to $-|\mathcal{A}|$ for continuous actions, or $\log|\mathcal{A}|$ for discrete). The gradient of this objective adjusts $\alpha$ so that the actual policy entropy tracks the target over training.

The effect: if the policy becomes too deterministic (entropy falls below target), $\alpha$ increases automatically to incentivize more exploration. If the policy is too random, $\alpha$ decreases.

> [!example]- Temperature Annealing Effect
> At the beginning of training, a high $\alpha$ keeps the policy random, driving broad exploration. As the agent learns which states are valuable, entropy naturally decreases. The autotuned mechanism detects this and gradually reduces $\alpha$, shifting from exploration to exploitation automatically — similar in spirit to $\varepsilon$-greedy annealing in DQN but grounded in a principled objective.

> [!warning] Common Misconception
> $\alpha$ in SAC is called "temperature" (by analogy with Boltzmann distributions / simulated annealing) but is **not** the learning rate. Confusing the two is a common mistake: $\alpha$ scales the entropy bonus; the learning rate scales the gradient step. They are entirely separate hyperparameters.

## Significance

The autotuned temperature variant (SAC v2) largely eliminates the most sensitive hyperparameter from SAC, making the algorithm robust across diverse environments without manual tuning. This is a key reason SAC achieves "similar performance across different random seeds" — the adaptive temperature compensates for reward scale differences between environments automatically.
