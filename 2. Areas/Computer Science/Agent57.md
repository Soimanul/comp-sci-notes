**Tags:** #concept #rl
**Related:** [[Advanced RL Techniques]], [[Intrinsic Rewards]], [[Universal Value Function Approximators]], [[Exploration-Exploitation Tradeoff]]

## Definition

Agent57 (Badia et al. 2020) is the first deep RL agent to surpass the standard human benchmark on **all 57 Atari games**, including games that had resisted RL progress for years (Pitfall!, Montezuma's Revenge). It achieves this by parameterising a family of policies ranging from fully exploratory to fully exploitative and using an adaptive meta-controller to select the best policy throughout training.

> [!info] Key Intuition
> Previous agents were either good on easy games (exploit-heavy) or good on hard games (explore-heavy), but never both. Agent57 trains *all possible exploration-exploitation trade-offs simultaneously* with a shared network, then adaptively chooses which one to prioritise — combining the strengths of all approaches without sacrificing any.

## Architecture

Agent57 builds on the Never Give Up (NGU) exploration framework and adds:

**Policy family via UVFA**: a single neural network parameterises $N$ distinct policies indexed by $(\beta_j, \gamma_j)$ — pairs of intrinsic reward scale and discount factor. Policy $j$ ranges from fully exploratory (high $\beta$, low $\gamma$) to fully exploitative ($\beta = 0$, high $\gamma$).

**Adaptive meta-controller (bandit)**: a non-stationary multi-armed bandit selects which policy index $j$ to prioritise during training. As training progresses, the meta-controller shifts weight toward more exploitative policies once the agent has discovered rewards through exploration.

**Distributed setup**:
- **Actors**: run agent + environment + intrinsic motivation; generate transitions
- **Replay buffer**: stores transitions with initial priorities
- **Learner**: minimises RL + intrinsic motivation losses via prioritised sampling; updates network weights; sends weights back to actors

## Benchmark Context

The 5th percentile analysis reveals the difficulty of hard exploration games:
- Agents like MuZero and R2D2 achieve near-zero performance on the hardest 5% of Atari games (Pitfall!, etc.)
- Agent57 is the first agent to score above human average on *all* games simultaneously, achieving ~120% of human normalised score at the 5th percentile

## DQN Lineage

Agent57 is the culmination of a sequence of improvements to DQN (2015):

$$\text{DQN} \xrightarrow{+\text{LSTM, Distributed}} \text{R2D2} \xrightarrow{+\text{Episodic Memory, RND}} \text{NGU} \xrightarrow{+\text{UVFA, Adaptive Bandit}} \text{Agent57}$$

> [!example]- Pitfall! Before and After Agent57
> Pitfall! is a notoriously hard Atari game requiring complex sequential exploration through a large maze to find rewards. All prior deep RL methods scored 0 on average — the maze is too large for random exploration to ever find a reward. NGU was the first to achieve non-zero rewards (mean 8,400); Agent57 achieves consistent super-human performance by combining NGU's exploration with adaptive policy selection.

> [!warning] Common Misconception
> Agent57 surpasses the human benchmark on all 57 games by average score, but the headline metric is the 5th percentile — meaning it outperforms humans even on the *hardest* games. Prior agents had high average scores because they dominated easy games, masking catastrophic failure on hard exploration games.

## Significance

Agent57 closed a 5-year benchmark gap and validated the approach of combining intrinsic motivation, recurrent memory, and adaptive policy selection. It establishes that hard exploration problems are not fundamentally intractable — they require the right combination of novelty signals and meta-level policy selection.
