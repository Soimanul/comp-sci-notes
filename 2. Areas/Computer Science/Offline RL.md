**Tags:** #concept #rl
**Related:** [[Advanced RL Techniques]], [[Reinforcement Learning]], [[Model-Based vs Model-Free RL]]

## Definition

Offline RL (also called batch RL) is a reinforcement learning paradigm in which the agent learns entirely from a fixed, pre-collected dataset without any interaction with the environment during training. The agent cannot query the environment to explore or verify counterfactual actions.

> [!info] Key Intuition
> Offline RL is to online RL what supervised learning is to active learning: the agent must extract everything it needs from a static dataset, which means it cannot recover from gaps or errors in that data by exploring further.

## The Core Challenge: Distributional Shift

Standard off-policy algorithms (DQN, DDPG) learn from data collected by a different policy, but can correct errors by collecting new data. In offline RL, this feedback loop is severed. When the learned policy visits state-action pairs that are **out-of-distribution** relative to the dataset, the value function produces overconfident, spurious estimates — a phenomenon called distributional shift.

The agent faces **counterfactual queries**: it must estimate "what would have happened if I had taken a different action?" without ever being able to try that action. This is inherently unreliable when the dataset does not cover the state-action space well.

## Solution Families

| Family | Approach | Examples |
|---|---|---|
| **Policy constraints** | Constrain the learned policy to stay close to the behaviour policy | BCQ, BEAR, BRAC, AWAC |
| **Conservative value estimation** | Penalise Q-values for out-of-distribution actions | CQL (Conservative Q-Learning) |
| **Uncertainty estimation** | Quantify model uncertainty and avoid high-uncertainty regions | Ensemble methods, Bayesian RL |

## S4RL: Data Augmentation for Offline RL

S4RL addresses offline RL's limited data by augmenting the static dataset with seven synthetic transition schemes:
- Gaussian noise, uniform noise, amplitude scaling, dimension dropout, state-switch, state mix-up, adversarial state training

Each augmented transition $(s', a, r, s'')$ preserves the original $(a, r)$ but perturbs the state representation, synthetically expanding the coverage of the dataset.

## D4RL Benchmark

D4RL is the standard benchmark for offline RL, providing fixed datasets of varying quality (random, medium, expert, mixed) across continuous control tasks (HalfCheetah, Hopper, Walker). It enables apples-to-apples comparison of offline RL algorithms.

> [!example]- V-PTR: Video Pre-Training for Robotic Offline RL
> V-PTR (Video Pre-Training for Robots) is a three-stage offline RL pipeline:
> 1. **Pre-train** on Ego4D (4M human video transitions) using TD learning to learn general visual representations.
> 2. **Offline RL** on the Bridge dataset (robot demonstrations) to learn robotic manipulation.
> 3. **Fine-tune** on the target task.
> The key insight: pre-training on human video provides rich state representations that transfer to robotic control, dramatically reducing the amount of robot demonstration data required.

> [!warning] Common Misconception
> Offline RL is not simply applying any off-policy algorithm to a static dataset. Standard off-policy algorithms like DQN assume the ability to collect corrective data; without it, they diverge due to bootstrapping on out-of-distribution Q-values. Offline RL requires specific algorithmic modifications to be stable.

## Significance

Offline RL is essential when online data collection is expensive (robotics), dangerous (clinical treatment), or unethical (patient trials). The paradigm shift from online to offline RL is as significant as the shift from supervised to self-supervised learning.
