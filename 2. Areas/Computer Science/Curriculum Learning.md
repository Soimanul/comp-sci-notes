**Tags:** #concept #rl
**Related:** [[Reinforcement Learning]], [[Reward Hypothesis]], [[NEAT]], [[Intermediate Practice]]

## Definition

Curriculum Learning is a training strategy in which an agent is exposed to tasks of increasing difficulty, or with intermediate reward signals, rather than being trained on the full final task from the start.

> [!info] Key Intuition
> Just as a student learns arithmetic before calculus, an RL agent learns faster when hard tasks are broken into achievable sub-goals — sparse or delayed rewards are replaced by a structured sequence of denser, intermediate rewards.

## How It Works

In RL, curriculum learning typically involves:

- **Intermediate goals**: define sub-task milestones (e.g. reach checkpoint A before attempting the full race track) that generate reward signals earlier in training
- **Save/Load continuity**: train on a simple version, save the model, then load it and continue training on progressively harder versions
- **Staged environment difficulty**: start with easy track layouts, obstacles removed, or shorter episodes, then incrementally increase challenge

In the PyRace context, curriculum learning addresses the problem of sparse rewards: if a car only receives a reward for completing a lap, early training yields no useful signal because the car crashes immediately. Introducing intermediate distance-based rewards guides learning before the agent can complete the full task.

> [!example]- PyRace Curriculum
> Stage 1: Train on a straight segment — reward for not crashing.
> Stage 2: Load Stage 1 weights; train on a track with one bend.
> Stage 3: Load Stage 2 weights; train on the full circuit.
> This staged approach compresses the number of episodes needed for convergence vs training on the full circuit from scratch.

> [!warning] Common Misconception
> Curriculum Learning is a training strategy, not an algorithm. It does not change the underlying learning algorithm (Q-table, PPO, NEAT) — it changes the *sequence of environments or reward shaping* the agent encounters. It can be applied to any RL method.

## Significance

Curriculum learning is essential for any RL problem with sparse rewards, long horizons, or large state spaces where random exploration is unlikely to discover rewarding transitions. It is directly applicable to robotics, autonomous driving, and complex game environments.

## From RL Applications

Curriculum Learning and [[Apprenticeship Learning]] are complementary strategies with an explicit trade-off: curriculum learning guides exploration through structured difficulty progression (no expert needed); apprenticeship learning constrains exploration through expert demonstrations (expert needed, but faster convergence and safer exploration). In practice, they are combined: expert demos bootstrap the curriculum's first stage, then difficulty is escalated progressively.
