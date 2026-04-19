**Tags:** #topic #hub #rl
**Related:** [[Reinforcement Learning]], [[Gymnasium Environment]], [[Markov Decision Process]]

## Overview

Practical RL development connects three components: a simulation or real-world environment, an RL algorithm library, and an agent design that bridges the two. This hub covers the landscape of RL frameworks and environment platforms — how to classify them, evaluate them, and the key tools used in practice, from general-purpose libraries like Stable Baselines3 and RLlib, to domain-specific environments for robotics, finance, autonomous driving, and multi-agent settings.

> [!abstract]- TL;DR
> RL frameworks are evaluated along five axes — development status, utility (algorithm breadth), modularity, documentation, and ecosystem — with ray[rllib] scoring highest overall. The standard environment API is OpenAI Gym / Gymnasium, which almost all libraries support, making environment and algorithm interchangeable.

## Knowledge Map

### 1. Framework Concepts
- [[Stable Baselines3]]
- [[RLlib]]
- [[Vectorized Environments]]
- [[Logging and Monitoring RL]]
- [[Hyperparameter Tuning for RL]]

### 2. Environment Design
- [[Gymnasium Environment]]
- [[Custom Environment Design]]
- [[Reward Shaping]]

### 3. Framework Taxonomy
- **Technical** — algorithms, environment standardisation, performance monitoring (e.g. Stable Baselines3, RLlib, TF-Agents, Tianshou)
- **Functional** — problem-type oriented (e.g. FinRL for trading, CARLA for autonomous driving, RLCard for card games)
- **Applied** — project or hardware oriented (e.g. simulation + sensor integration, Duckietown, RWARE)

### 4. Notable Environments by Domain
- **Robotics**: Gymnasium-Robotics, PyBullet, MuJoCo, CARLA
- **Games / Multi-Agent**: PettingZoo, Melting Pot, StarCraft SMAC, RLCard
- **Finance / Trading**: FinRL, Gym-Anytrading, Phantom (financial markets)
- **Autonomous Driving**: CARLA, highway-env, CityFlow, Duckietown
- **Logistics**: RWARE (multi-robot warehouse)
- **LLM Fine-Tuning (RLHF)**: TRLX, RL4LMs

> [!question]- Common Exam Questions
> - What are the five criteria used to compare deep RL frameworks, and which framework scored highest?
> - What is the role of the Gymnasium API, and why do most RL libraries support it?
> - Distinguish between a "technical", "functional", and "applied" RL framework.
> - What makes RLlib particularly suited to distributed RL training?
