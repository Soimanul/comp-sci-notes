**Tags:** #concept #rl
**Related:** [[Advanced RL Techniques]], [[Exploration-Exploitation Tradeoff]], [[Reward Shaping]]

## Definition

Intrinsic rewards are internally generated reward signals that encourage an agent to explore its environment independent of any task-specific reward. The total reward is decomposed as:

$$R = R_\text{intrinsic} + R_\text{extrinsic}$$

where $R_\text{extrinsic}$ is the sparse environment reward and $R_\text{intrinsic}$ is a dense, self-generated novelty signal.

> [!info] Key Intuition
> Intrinsic motivation solves the sparse reward problem by giving the agent a reason to explore *before* it ever receives task reward — the agent is curious about the world, not just goal-directed.

## Taxonomy of Intrinsic Motivation

| Type | Signal | Timescale |
|---|---|---|
| **Curiosity** | Prediction error of a forward model | Per-step |
| **Novelty** | Inverse visit count approximation | Lifetime |
| **Episodic novelty** | Distance to nearest visited state this episode | Per-episode |
| **Life-long novelty** | Distance to nearest visited state across all training | Lifetime |

## Random Network Distillation (RND)

RND (Burda et al. 2018) solves a key problem with curiosity-based methods: prediction error is high not only for unvisited states but also for states with stochastic dynamics, model misspecification, and learning instabilities.

**Solution**: instead of predicting environment dynamics, predict the output of a **fixed randomly-initialized network**:
- **Target network** $g$: fixed random weights; outputs a vector for each state
- **Predictor network** $\hat{g}$: trained to match $g$'s output

$$r^i_t = \|\hat{g}(x_t) - g(x_t)\|^2$$

Since $g$ is fixed and deterministic, the prediction error is high only for states not visited frequently — eliminating all spurious sources of prediction error. RND achieves state-of-the-art on Montezuma's Revenge without demonstrations.

## Never Give Up Architecture

Never Give Up (NGU, Badia et al. 2020) combines two complementary novelty modules:

**Episodic novelty module** (short-term memory):
- Embeds the current state via an inverse dynamics embedding network
- Computes $r^{\text{episodic}}_t$ as inverse distance to k-nearest neighbours in the episodic memory buffer $M$
- Resets each episode — rewards revisiting states that were interesting early in the episode

**Life-long novelty module** (RND):
- Computes $\alpha_t = |\hat{g}(x_t) - g(x_t)|^2$ as the life-long novelty signal
- Does not reset — penalises states that have been frequently visited across all training

The intrinsic reward combines both via multiplicative modulation:
$$r^i_t = r^{\text{episodic}}_t \cdot \alpha_t$$

NGU doubles the performance of the base agent on hard exploration Atari games and is the first algorithm to achieve non-zero reward on Pitfall! without demonstrations (mean score 8,400).

> [!example]- IAC: Learning Progress as Intrinsic Reward
> Intelligent Adaptive Curiosity (Oudeyer et al. 2007) defines intrinsic reward as **learning progress**: $LP = \langle E(t+1) \rangle - \langle E(t) \rangle$, the decrease in prediction error from one time window to the next. This motivates the agent toward situations where it is *actively learning*, not just toward novel or uncertain states — avoiding the trivial strategy of staring at unpredictable noise (which yields high curiosity but zero learning progress).

> [!warning] Common Misconception
> Intrinsic rewards based purely on prediction error reward staring at noise: a TV showing random static is maximally surprising every frame. RND avoids this by predicting a *fixed* random network output — stochastic environments produce consistently high error from the target network's perspective and are not artificially rewarded. IAC avoids it by rewarding *learning progress*, not prediction error magnitude.

## Significance

Intrinsic rewards are essential for hard exploration problems where extrinsic reward is so sparse that random exploration never discovers it. They are the mechanism behind some of the most spectacular RL results: NGU and Agent57's performance on games that stumped all prior methods for years.
