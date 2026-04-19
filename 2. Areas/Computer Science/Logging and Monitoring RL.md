**Tags:** #concept #rl
**Related:** [[RL Frameworks]], [[Stable Baselines3]], [[RLlib]], [[Hyperparameter Tuning for RL]]

## Definition

Logging and monitoring in RL is the practice of recording training metrics — episode returns, policy loss, value loss, entropy, and environment-specific signals — and visualising them in real time or post-hoc to diagnose training health and guide iterative improvement.

> [!info] Key Intuition
> RL training curves are noisy and non-monotonic by nature. Without structured logging you cannot distinguish a policy that is genuinely learning from one that is stuck or diverging — monitoring is your window into the training process.

## Key Metrics to Track

| Metric | What it tells you |
|---|---|
| Episode reward mean | Primary measure of policy quality |
| Episode length mean | Useful for time-limited tasks |
| Policy loss | Should decrease or stabilise; spikes indicate instability |
| Value function loss | Should decrease; divergence is a warning sign |
| Entropy / KL divergence | Low entropy = premature convergence; high KL = too-large policy updates |
| Explained variance | How well the value function predicts returns |

## Primary Tools

### TensorBoard
TensorBoard is the standard logging backend for both Stable Baselines3 and RLlib. Training runs write scalar summaries to a log directory; the dashboard displays interactive time-series plots.

```python
# SB3: enable TensorBoard logging
model = PPO("MlpPolicy", env, tensorboard_log="./tb_logs/")
model.learn(total_timesteps=100_000)
# Launch: tensorboard --logdir ./tb_logs/
```

### Weights & Biases (W&B)
Cloud-based experiment tracking platform. Supports hyperparameter sweeps, model artefact versioning, and team collaboration. Both SB3 and RLlib have W&B callback integrations.

### Neptune
Alternative to W&B; similar feature set. Cited in the lecture as a logging/tracking tool alongside TensorBoard.

## Callbacks in SB3

SB3 exposes a `BaseCallback` interface that fires at each training step or episode. Common built-in callbacks:

- `EvalCallback`: periodically evaluates the policy on a separate environment and saves the best model
- `CheckpointCallback`: saves the model every $n$ steps
- `StopTrainingOnRewardThreshold`: early stopping when a reward target is reached

> [!example]- EvalCallback Pattern
> ```python
> from stable_baselines3.common.callbacks import EvalCallback
> import gymnasium as gym
>
> eval_env = gym.make("LunarLander-v2")
> callback = EvalCallback(eval_env, best_model_save_path="./best_model/",
>                         eval_freq=5000, n_eval_episodes=10)
> model.learn(total_timesteps=200_000, callback=callback)
> ```

> [!warning] Common Misconception
> The training reward curve is not the same as the evaluation reward curve. Training rewards are noisy, exploration-inflated estimates; the evaluation curve (from deterministic policy rollouts on a separate environment) is the true measure of policy quality.

## Significance

Structured logging is what makes RL experiments reproducible and debuggable. The ability to spot reward divergence, entropy collapse, or value function instability early saves days of wasted compute. Logging quality is one of the explicit criteria (criterion 5) used to evaluate RL libraries.
