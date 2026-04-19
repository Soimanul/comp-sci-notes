**Tags:** #concept #rl
**Related:** [[Maximum Entropy RL]], [[Soft Actor-Critic (SAC)]], [[Temperature Parameter in SAC]], [[Proximal Policy Optimization]], [[Exploration-Exploitation Tradeoff]], [[Research Papers and Innovation Trends B]]

## Definition

Entropy Regularization in RL is the practice of adding the entropy of the current policy's action distribution as a bonus term to the loss function or reward, incentivizing the policy to maintain randomness (exploration) and discouraging premature convergence to a deterministic strategy.

> [!info] Key Intuition
> Without entropy regularization, a policy will eventually collapse to always picking the action with the highest estimated value, ignoring all alternatives. Entropy regularization penalizes this collapse, keeping the policy diverse — which is especially valuable early in training when value estimates are noisy.

## How It Works

The entropy of a policy at state $s$ is:

$$H(\pi(\cdot|s)) = -\mathbb{E}_{a \sim \pi}\!\left[\log \pi(a|s)\right]$$

- **High entropy**: the policy is near-uniform (many actions have similar probability). Maximum randomness.
- **Low entropy**: the policy is near-deterministic (one action dominates). Minimum randomness.

### In PPO

PPO adds an entropy bonus to the combined loss:

$$L^{\text{CLIP+VF+S}}_t(\theta) = \hat{\mathbb{E}}_t\!\left[L^{\text{CLIP}}_t(\theta) - c_1 L^{\text{VF}}_t(\theta) + c_2 S[\pi_\theta](s_t)\right]$$

where $c_2$ is a small coefficient (e.g. 0.01) and $S[\pi_\theta](s_t)$ is the entropy at the current state. The entropy is evaluated by the `evaluate` function, which returns value, log-probabilities, and entropy of the mini-batch.

For discrete action spaces, the strength of entropy regularization is controlled by the `beta` hyperparameter (typical range 1e-4 to 1e-2). During healthy training, entropy should **decrease gradually** as the policy becomes more confident; if it drops too quickly, increase `beta`.

### In SAC

In SAC, entropy regularization is a core part of the objective, not an auxiliary trick. The temperature $\alpha$ scales the entropy term, making it a first-class citizen alongside the reward signal. See [[Temperature Parameter in SAC]] and [[Maximum Entropy RL]].

> [!example]- Entropy Collapse in Practice
> Without entropy regularization, a PPO agent on a game with multiple viable strategies often converges to a single strategy — which may work well on familiar scenarios but fail catastrophically on novel ones. Adding even a small entropy bonus (c2 = 0.01) keeps the policy slightly stochastic, improving generalization. In TensorBoard, the `entropy_loss` curve should drift upward (negation convention: more negative = higher entropy) over training.

> [!warning] Common Misconception
> Entropy regularization does not mean the policy will always be random. At convergence, the policy naturally settles to a distribution that balances reward maximization and entropy. If a single action dominates by a large margin, the policy still concentrates probability on it — it just does not assign zero probability to alternatives.

## Significance

Entropy regularization is one of the key "lines of development for the improvement of RL algorithms" identified in the research literature. It addresses the exploration problem without requiring explicit exploration bonuses or count-based methods. In PPO it is an optional but recommended trick; in SAC it is structural — SAC would not be SAC without it.
