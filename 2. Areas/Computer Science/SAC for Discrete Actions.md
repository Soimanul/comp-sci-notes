**Tags:** #concept #rl
**Related:** [[Soft Actor-Critic (SAC)]], [[Maximum Entropy RL]], [[Temperature Parameter in SAC]], [[Research Papers and Innovation Trends B]]

## Definition

SAC for Discrete Actions is an adaptation of the Soft Actor-Critic algorithm to environments with discrete (finite) action spaces, introduced by Christodoulou (2019). The original SAC formulation relies on a reparameterization trick with a squashed Gaussian distribution, which is not applicable to discrete actions. The discrete variant modifies the policy update rule to work directly with categorical distributions.

> [!info] Key Intuition
> In continuous SAC, the policy outputs a Gaussian mean and standard deviation and actions are sampled differentiably. For discrete actions, the policy instead outputs a softmax probability vector over all actions — and the expectation over actions can be computed exactly (no sampling needed), which actually simplifies the gradient computation.

## The Modification

In continuous SAC, the actor loss is:

$$\mathcal{L}_\phi = \mathbb{E}_{s}\!\left[\alpha \log \pi_\phi(a|s) - Q(s,a)\right]$$

where $a$ is sampled via the reparameterization trick.

In discrete SAC, since the action space is finite with $|\mathcal{A}|$ elements, the expectation is computed exactly:

$$\mathcal{L}_\phi = \mathbb{E}_{s}\!\left[\sum_{a} \pi_\phi(a|s)\!\left(\alpha \log \pi_\phi(a|s) - Q(s,a)\right)\right]$$

The Q-network also changes: instead of taking a single $(s,a)$ input and outputting one value, it takes only $s$ and outputs a vector of Q-values of size $|\mathcal{A}|$ — one per action. This matches the DQN critic architecture.

### Why Standard SAC Fails for Discrete Actions

The reparameterization trick samples $a = f(\epsilon, s)$ where $\epsilon$ is Gaussian noise. For discrete actions, there is no differentiable mapping from Gaussian noise to a categorical sample — the Gumbel-Softmax relaxation exists but introduces bias. The discrete SAC variant sidesteps this entirely by using the explicit expectation.

> [!example]- Atari Benchmark
> Christodoulou (2019) validated discrete SAC on Atari games. Without any hyperparameter tuning, discrete SAC was competitive with tuned model-free baselines across multiple games from the Atari suite — demonstrating that the entropy regularization framework generalizes well beyond continuous robotics to high-dimensional discrete game environments.

## Significance

Discrete SAC extends the maximum entropy RL framework to the large class of environments with discrete action spaces (Atari, board games, many real-world decision problems). In Stable Baselines 3, the standard SAC implementation only supports continuous action spaces; discrete SAC requires a slightly modified implementation. This makes the algorithm applicable across virtually all standard RL benchmark environments.
