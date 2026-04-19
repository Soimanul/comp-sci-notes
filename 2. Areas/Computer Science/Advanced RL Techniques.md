**Tags:** #hub #rl
**Related:** [[Reinforcement Learning]], [[Y3S2 - Reinforcement Learning]]

## Overview

This hub covers the frontier of modern reinforcement learning research: paradigms that extend the standard online MDP setting to handle real-world constraints — no online interaction, no explicit reward, sparse feedback, and the need for scalable architectures that unify perception, memory, learning, and action.

> [!abstract]- TL;DR
> Modern RL research moves in two directions simultaneously: solving the *data problem* (offline RL, imitation learning, data augmentation) and solving the *exploration problem* (intrinsic rewards, HER, novelty-based exploration). Cutting-edge architectures like Dreamer, JEPA, and Active Inference aim to unify these threads into coherent systems that learn efficiently from experience without explicit reward engineering.

## Knowledge Map

### 1. Offline RL and Data-Efficient Learning
- [[Offline RL]]
- [[World Models]]
- [[Inverse Reinforcement Learning]]

### 2. Advanced Exploration
- [[Hindsight Experience Replay]]
- [[Intrinsic Rewards]]
- [[Universal Value Function Approximators]]
- [[Agent57]]

### 3. Frontier Architectures
- [[Active Inference]]
- [[JEPA]]

> [!question]- Common Exam Questions
> - What is the distributional shift problem in offline RL, and what are the three families of solutions?
> - How does Hindsight Experience Replay turn failure into a learning signal without reward engineering?
> - What is the difference between an episodic novelty module and a life-long novelty module in Never Give Up?
> - How does Active Inference unify perception, learning, and action into a single loop?
> - What is JEPA's Mode-1 vs Mode-2, and why does Mode-2 require amortized inference?
