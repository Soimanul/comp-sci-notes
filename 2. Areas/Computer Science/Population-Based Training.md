**Tags:** #concept #rl
**Related:** [[Evolutionary Computation]], [[Neuroevolution]], [[OpenAI ES]], [[Reinforcement Learning]], [[Hyperparameter Tuning]]

## Definition

Population-Based Training (PBT) is a hyperparameter optimisation method that trains a population of models in parallel and periodically applies evolutionary operations (selection and mutation) to transfer weights and hyperparameters from better-performing models to worse-performing ones, all during training.

> [!info] Key Intuition
> PBT is the evolutionary analogue of online hyperparameter optimisation: instead of first finding good hyperparameters and then training, it discovers good hyperparameters and adapts them throughout training — combining the benefits of random search with the efficiency of hand-tuning.

## How It Works

PBT interleaves three operations:

1. **Step**: each worker in the population trains its model for a fixed number of steps using its current hyperparameters.
2. **Exploit**: periodically evaluate all workers; poorly performing workers copy the weights and hyperparameters of a better-performing worker (tournament selection or truncation selection).
3. **Explore**: after copying, the hyperparameters are perturbed (mutated) slightly — e.g. learning rate is multiplied by a random factor in $[0.8, 1.2]$.

Because weights are copied (not just hyperparameters), PBT effectively allows poor workers to "jump" to a better region of parameter space and then diverge from there with a new set of hyperparameters.

### Comparison to Other Hyperparameter Optimisation Methods

| Method | Hyperparameter tuning | Weight training |
|---|---|---|
| Grid/random search | Sequential: tune then train | Separate |
| Bayesian optimisation | Sequential: tune then train | Separate |
| **PBT** | Online: tune during training | Integrated |

> [!example]- PBT in RL (Jaderberg et al., DeepMind 2017)
> A population of 20 A3C agents is trained in parallel on Atari. Every 10,000 steps, the bottom 20% of agents (by episode reward) copy weights and hyperparameters from the top 20%, then perturb learning rate and entropy bonus. The result outperforms individually tuned baselines.

> [!warning] Common Misconception
> PBT is **not** just parallel random restarts. The key innovation is weight inheritance: workers do not restart from scratch after exploit/explore — they continue training from the inherited weights. This means PBT can adapt hyperparameters in a way that is sensitive to the current stage of training.

## Significance

PBT is widely used at DeepMind and Google Brain to train large RL agents (AlphaStar, AlphaFold). It bridges evolutionary computation and modern deep learning by applying population-level selection pressure to the training process itself rather than to end-of-training performance.
