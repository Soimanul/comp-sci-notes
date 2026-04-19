**Tags:** #concept #rl
**Related:** [[Advanced RL Techniques]], [[Curriculum Learning]], [[Exploration-Exploitation Tradeoff]]

## Definition

Hindsight Experience Replay (HER) is a technique for learning from sparse, binary rewards by augmenting the replay buffer with **imagined trajectories**: failed episodes are replayed with the actual achieved endpoint substituted as the goal, so the agent always has positive reward to learn from regardless of policy quality.

> [!info] Key Intuition
> When you fail to reach your intended goal, you still succeeded at *reaching where you ended up* — HER exploits this by asking "what if this had been my goal all along?" and storing that counterfactual as a second, successful training example alongside the real failure.

## Mechanism

Standard replay buffer stores tuples $(s_t, G, a_t, r_t, s_{t+1})$ where $G$ is the desired goal. When an episode reaches terminal state $S'$ without achieving $G$:

1. Cache the original trajectory: $\{(S_0, G, a_0, r_0, S_1), \ldots, (S_n, G, a_n, r_n, S')\}$
2. Also cache an **imagined trajectory** with $G$ replaced by $S'$: $\{(S_0, S', a_0, r_0, S_1), \ldots, (S_n, S', a_n, r_n, S')\}$

In the imagined trajectory, the final reward at step $n$ is now positive (the agent "reached its goal" $S'$). HER requires off-policy learning so it can train on both the real and imagined trajectories — compatible with DQN, SAC, TD3, and DDPG.

## Generalisation Through Imagined Goals

Initially, the only goals the agent can achieve are states reachable by a random policy — which are useless. But neural network function approximation **generalises**: learning to reach $S'$ teaches the agent something about reaching nearby states. As the agent improves, it can reach states progressively farther from the start, until it eventually learns to reach the true goal. HER creates an **implicit curriculum** without any manual difficulty scheduling.

## HER vs Curriculum Learning

| Property | HER | Curriculum Learning |
|---|---|---|
| Goal sequencing | Automatic (uses achieved states) | Manual (designer creates easier instances) |
| Engineering required | None — works with any off-policy algorithm | Significant — need simpler task versions |
| Mechanism | Relabels replay buffer; implicit curriculum | Explicit staged training environments |

HER is strictly complementary to curriculum learning: HER handles the reward signal problem; curriculum learning handles the difficulty sequencing problem.

> [!example]- Robotic Manipulation with Binary Rewards
> In the original paper, a robotic arm must push/slide/pick-and-place objects to a target position. The reward is binary: +1 if object reaches goal (within tolerance), 0 otherwise. Without HER, the agent never receives a positive reward and learns nothing. With HER, every episode provides at least one positive example (the achieved endpoint), and the policy trained in simulation transfers to physical hardware.

> [!warning] Common Misconception
> HER does not change the reward function — it relabels the *goal* in the replay buffer, which changes what counts as success for each stored transition. The reward function itself (binary +1/0 at goal) remains unchanged. This is why HER avoids the pitfalls of reward shaping: it doesn't add proxy rewards, it simply exploits the multi-goal structure of the task.

## Significance

HER eliminates the need for reward engineering in multi-goal environments with sparse binary rewards. It is one of the most practically impactful techniques in robotic RL, enabling training from binary success/failure signals that would otherwise be too sparse for learning.
