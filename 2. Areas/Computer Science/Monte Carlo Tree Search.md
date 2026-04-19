**Tags:** #concept #rl
**Related:** [[Learning and Planning]], [[Monte Carlo Methods]], [[Model-Based vs Model-Free RL]], [[Q-Learning]]

## Definition

Monte Carlo Tree Search (MCTS) is a decision-time planning algorithm that selects actions by incrementally building a search tree rooted at the current state, using Monte Carlo simulations to estimate action values for nodes in the tree. It is an **anytime** algorithm: it can be terminated at any point and still return the best action found so far.

> [!info] Key Intuition
> Instead of learning a value function once and using it everywhere, MCTS re-plans from scratch at every decision point — spending its entire computational budget evaluating actions only for the state the agent is actually in right now.

## Four Phases (per iteration)

Each MCTS iteration repeats the following four steps until a computational budget (time limit or node count) is exhausted:

1. **Selection**: Starting at the root (current state), traverse the tree by repeatedly selecting child nodes using the **tree policy** (e.g. UCT) until reaching a node that is not fully expanded.
2. **Expansion**: Add one or more child nodes to the selected leaf by applying an unexplored action.
3. **Simulation**: From the newly expanded node, run a complete rollout to a terminal state using the **rollout policy** (often random or a fast heuristic). This produces a Monte Carlo return estimate.
4. **Backup (Backpropagation)**: Propagate the return back up the tree, updating the action-value estimates $Q(s,a)$ of every node traversed during selection.

After the budget is exhausted, the action with the highest $Q$ value at the root is executed. The tree is then discarded (or partially retained) and the process begins anew from the next state.

## Upper Confidence Trees (UCT)

The tree policy uses UCT — MCTS combined with the UCB1 multi-armed bandit strategy — to balance exploration and exploitation during selection:

$$\text{argmax}_{a \in \mathcal{A}(s)}\; Q(s,a) + 2C_p\sqrt{\frac{2\ln N(s)}{N(s,a)}}$$

where $N(s)$ is the visit count of state node $s$, $N(s,a)$ is the number of times action $a$ was selected from $s$, and $C_p > 0$ is an exploration constant. When $Q(s,a) \in [0,1]$ and $C_p = 1/\sqrt{2}$, UCT converges to the **Minimax** algorithm in two-player zero-sum games.

> [!example]- AlphaGo / AlphaZero
> AlphaGo (2016) defeated 18-time Go world champion Lee Sedol by combining MCTS with deep neural networks. The policy network guides the **selection** step by prioritising promising branches; the value network replaces full rollouts in the **simulation** step. AlphaZero generalised this approach, learning both networks from self-play alone (no human game data), and achieved superhuman performance in Go, Chess, and Shogi.
>
> Go has approximately $10^{170}$ valid states — far beyond exhaustive search. AlphaGo evaluates ~30 million simulations per move, exploring a tiny but strategically focused fraction of the tree.

> [!warning] Memory vs. Statelessness Trade-off
> Basic MCTS does not retain value functions or policies between successive decisions — each new state triggers a fresh search. In practice many implementations carry over portions of the tree (subtrees reachable from the chosen action) to amortise computation, but this is optional. The key distinction from background-planning methods like Dyna is that MCTS computation is always tied to the **current** decision.

## Significance

MCTS is the dominant algorithm for decision-time planning in large discrete state spaces. It requires only a sample model (no distribution model), scales gracefully with computation, and naturally handles environments too large for global value-function methods. Its integration with deep RL (AlphaGo/AlphaZero) represents the state of the art in game-playing AI.
