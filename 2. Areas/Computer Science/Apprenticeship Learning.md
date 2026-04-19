**Tags:** #concept #rl
**Related:** [[RL Applications]], [[Curriculum Learning]], [[Reinforcement Learning]], [[Reward Shaping]]

## Definition

**Apprenticeship Learning** (also called imitation learning) is a training strategy in which an RL agent learns by observing and imitating expert demonstrations, rather than by optimising a reward signal from scratch. The agent uses expert exemplars to constrain the initial state space explored during learning.

> [!info] Key Intuition
> Show the agent what good looks like before asking it to discover good on its own — expert demonstrations act as a compressed curriculum, biasing exploration toward high-reward regions of the state space.

## How It Works

1. **Collect demonstrations**: a human expert or existing controller executes the task, generating a dataset of $(s, a)$ pairs.
2. **Behavioural cloning** (simplest form): train a supervised policy $\pi(a|s)$ to mimic the demonstrations.
3. **Inverse RL** (more sophisticated): infer the reward function the expert was implicitly optimising, then use RL with that recovered reward.
4. **GAIL** (Generative Adversarial Imitation Learning): a discriminator distinguishes agent from expert trajectories; the agent optimises to fool the discriminator.

## Trade-offs

| Benefit | Cost |
|---|---|
| Constrains exploration to feasible, safe regions | Limits discovery of novel solutions the expert never demonstrated |
| Dramatically reduces sample complexity | Requires access to expert demonstrations (expensive or impossible for some tasks) |
| Provides a warm-start policy for further RL fine-tuning | Distributional shift: agent encounters states not covered by demonstrations and fails |

> [!example]- Robotics Warm Start
> For a robotic arm assembly task, a human teleoperates the arm to generate 100 demonstration trajectories. Behavioural cloning produces a policy that succeeds ~60% of the time. This policy is then used as the initialisation for PPO fine-tuning, which reaches ~95% success in far fewer episodes than PPO from a random initialisation.

> [!warning] Common Misconception
> Apprenticeship learning does not guarantee finding the optimal policy — it finds a policy that resembles the expert. If the expert is suboptimal or the demonstrations do not cover important edge cases, the agent will faithfully imitate those limitations.

## Significance

Apprenticeship Learning is especially valuable when exploration is dangerous (medical robots, autonomous vehicles) or when random exploration is too sample-inefficient to discover rewarding transitions. It trades the possibility of superhuman discovery for faster, safer convergence to expert-level performance.
