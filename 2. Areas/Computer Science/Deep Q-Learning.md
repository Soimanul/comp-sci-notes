**Tags:** #concept #rl
**Related:** [[Q-Learning]], [[Bellman Equation]], [[Action Value Function]], [[Exploration-Exploitation Tradeoff]], [[Integration of Concepts Practice]]

## Definition

Deep Q-Learning (DQL) extends tabular Q-learning by replacing the Q-table with a deep neural network that approximates the action-value function $Q(s, a; \theta)$. The network takes the current state as input and outputs a Q-value for each possible action.

> [!info] Key Intuition
> The neural network is taught to predict "how good is each action right now?" by repeatedly comparing its current prediction against a Bellman-equation-derived target — the loss is just the squared difference between the two.

## How It Works

The training loop follows four steps repeated until convergence:

1. **Initialise** Q-values (randomly initialise network weights $\theta$)
2. **Choose action**: $a = \arg\max_a \hat{Q}(s, a; \theta)$, or a random action with probability $\varepsilon$ (ε-greedy)
3. **Perform action**, observe reward $R$ and next state $s'$
4. **Update** network weights using the Bellman target:

$$Q_{\text{new}} = R + \gamma \cdot \max_{a'} Q(s', a')$$

The loss function is Mean Squared Error between the current estimate and the target:

$$\mathcal{L} = \left(Q_{\text{new}} - Q(s, a; \theta)\right)^2$$

Weights are updated via backpropagation on this loss.

### Snake Game Architecture (Example)

In the Snake implementation, the model is a feedforward network:
- **Input**: 11-dimensional binary state vector — 3 danger flags (straight, right, left), 4 direction flags, 4 food-direction flags
- **Hidden**: 1 hidden layer
- **Output**: 3 Q-values corresponding to actions [straight, right turn, left turn]

Rewards used: eat food = +10, game over = −10, distance to food = −Δdist.

> [!example]- Worked Example
> State: [0, 0, 0, 0, 1, 0, 0, 0, 1, 0, 1] (no danger, moving right, food down-right)
> Network predicts Q-values: [5.0, 2.7, 0.1]
> Action taken: straight (argmax → [1, 0, 0])
> Reward: +10 (ate food)
> Target: $Q_{\text{new}} = 10 + \gamma \cdot \max Q(s', \cdot)$
> Loss: $(Q_{\text{new}} - 5.0)^2$ → backprop updates weights.

> [!warning] Common Misconception
> The Bellman equation is used as a *training target*, not a closed-form solution. Because the target itself depends on the network being trained, training is bootstrapped — the target is non-stationary and can cause instability (addressed in full DQN with target networks and replay buffers).

## Significance

Deep Q-Learning scales Q-learning to high-dimensional, continuous state spaces where tabular methods are infeasible. It is the foundation of DeepMind's DQN (2015), which achieved superhuman performance on Atari games using pixel inputs. In practice, TD DQN achieves a moving-average score of ~31 on Snake after 1,000+ games, with constant per-step compute independent of board size $N$.
