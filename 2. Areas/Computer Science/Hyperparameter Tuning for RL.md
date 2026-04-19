**Tags:** #concept #rl
**Related:** [[RL Frameworks]], [[Stable Baselines3]], [[RLlib]], [[Proximal Policy Optimization]], [[Deep Q-Learning]]

## Definition

Hyperparameter tuning for RL is the process of searching for the combination of training configuration values — such as learning rate, discount factor, batch size, entropy coefficient, and network architecture — that maximises agent performance on a given environment.

> [!info] Key Intuition
> RL algorithms are far more sensitive to hyperparameters than supervised learning: a learning rate that works for CartPole may cause divergence on LunarLander. Systematic search, not manual guessing, is essential.

## Key Hyperparameters by Algorithm Type

| Category | Parameter | Typical Range |
|---|---|---|
| All | Learning rate $\alpha$ | $10^{-5}$ – $10^{-3}$ |
| All | Discount factor $\gamma$ | $0.9$ – $0.999$ |
| All | Batch size | $32$ – $2048$ |
| Policy gradient (PPO) | Clip ratio $\epsilon$ | $0.1$ – $0.3$ |
| Policy gradient (PPO) | Entropy coefficient | $0$ – $0.01$ |
| Q-learning (DQN) | Replay buffer size | $10^4$ – $10^6$ |
| Q-learning (DQN) | Target update frequency | $100$ – $10000$ steps |
| Actor-critic | $n$-step return | $1$ – $20$ |

## Tuning Methods

- **Manual search**: adjust based on learning curves; useful for intuition-building
- **Grid search**: exhaustive but expensive; only viable for 1–2 parameters
- **Random search**: more efficient than grid search; samples hyperparameters from distributions
- **Bayesian optimisation / HPO**: learns a surrogate model of the objective to guide search (used in RL Baselines3 Zoo via Optuna)
- **Population-Based Training (PBT)**: runs a population of agents in parallel and adapts hyperparameters during training (used in RLlib)

## RL Baselines3 Zoo Integration

SB3's companion tool RL Baselines3 Zoo provides:
- Pre-tuned hyperparameter sets for common environments
- `python train.py --algo ppo --env LunarLander-v2 --optimize` for automated HPO via Optuna
- Reproducible scripts and result logging

> [!example]- Optuna HPO with SB3 Zoo
> Running `python train.py --algo ppo --env CartPole-v1 --optimize --n-trials 100` launches 100 PPO training runs sampling hyperparameters (learning rate, clip range, n_steps, etc.) and reports the best configuration found.

> [!warning] Common Misconception
> Tuning hyperparameters on one environment does not transfer to another, even for the same algorithm. Always re-tune when switching environments — published hyperparameter tables are starting points, not solutions.

## Significance

Hyperparameter tuning is one of the primary sources of performance gap between a baseline and a state-of-the-art result. Tools like RL Baselines3 Zoo and RLlib's built-in HPO pipelines make systematic search accessible without custom infrastructure.
