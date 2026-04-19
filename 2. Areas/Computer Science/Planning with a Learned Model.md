**Tags:** #concept #rl
**Related:** [[Learning and Planning]], [[Model-Based vs Model-Free RL]], [[Dyna Architecture]], [[Dynamic Programming for RL]]

## Definition

Planning with a learned model is the practice of using a model of the environment — learned from real experience — as a substitute environment to generate simulated transitions, which are then used to update value functions without additional real interaction.

> [!info] Key Intuition
> Once you have learned "what usually happens when I take action $a$ in state $s$", you can rehearse many imagined scenarios cheaply, squeezing more learning out of each real experience.

## How It Works

A model $\text{Model}(s,a)$ stores the predicted next state $S'$ and reward $R$ for each observed state–action pair $(s,a)$. Two model types exist:

- **Distribution model**: stores the full transition distribution $p(s',r \mid s,a)$ — required by expected updates (DP).
- **Sample model**: returns a single sampled $(S', R)$ drawn according to the distribution — sufficient for sample updates (TD, Q-learning).

Sample models are generally easier to obtain. The planning loop applies a learning algorithm (e.g. one-step Q-learning) to simulated experience:

$$Q(S,A) \leftarrow Q(S,A) + \alpha\!\left[R + \gamma \max_{a} Q(S',a) - Q(S,A)\right]$$

where $(S,A,R,S')$ comes from the model rather than the real environment.

> [!example]- Random-Sample One-Step Q-Planning
> Loop:
> 1. Pick $S \in \mathcal{S}$, $A \in \mathcal{A}(S)$ at random.
> 2. Query $\text{Model}(S,A)$ to get sample $R$, $S'$.
> 3. Apply Q-learning update: $Q(S,A) \leftarrow Q(S,A) + \alpha[R + \gamma \max_a Q(S',a) - Q(S,A)]$.
>
> This converges to the optimal policy under the same conditions as tabular Q-learning on the real environment, provided each $(S,A)$ is sampled infinitely often and $\alpha$ decreases appropriately.

## Significance

Planning with a learned model bridges model-free and model-based RL: the model is not given but learned (like model-free), yet once available it is exploited for planning (like model-based). This is the core idea behind the Dyna architecture. The quality of planning is bounded by model accuracy — a biased model produces biased value estimates.
