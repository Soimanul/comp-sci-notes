**Tags:** #concept #rl
**Related:** [[Learning and Planning]], [[Dyna Architecture]], [[Q-Learning]], [[Planning with a Learned Model]]

## Definition

Dyna-Q is the canonical tabular instantiation of the [[Dyna Architecture]], combining one-step Q-learning as the direct RL method with a deterministic sample model and $n$ background planning steps per real time step.

> [!info] Key Intuition
> Dyna-Q runs Q-learning twice per real step: once on real experience (direct RL) and $n$ times on simulated experience drawn from the learned model (planning) — with no extra environment interactions.

## Algorithm

**Initialize** $Q(s,a)$ and $\text{Model}(s,a)$ for all $s \in \mathcal{S}$, $a \in \mathcal{A}(s)$.

**Loop forever:**
- (a) $S \leftarrow$ current (non-terminal) state
- (b) $A \leftarrow \varepsilon\text{-greedy}(S,Q)$
- (c) Take action $A$; observe $R$, $S'$
- (d) $Q(S,A) \leftarrow Q(S,A) + \alpha\!\left[R + \gamma\max_a Q(S',a) - Q(S,A)\right]$ — **Direct RL**
- (e) $\text{Model}(S,A) \leftarrow R, S'$ — **Model Learning** (assumes deterministic env)
- (f) Repeat $n$ times: — **Planning**
  - $S \leftarrow$ random previously observed state
  - $A \leftarrow$ random action previously taken in $S$
  - $R, S' \leftarrow \text{Model}(S,A)$
  - $Q(S,A) \leftarrow Q(S,A) + \alpha\!\left[R + \gamma\max_a Q(S',a) - Q(S,A)\right]$

Convergence conditions mirror tabular Q-learning: each $(s,a)$ visited infinitely often, $\alpha$ decreasing appropriately.

> [!example]- Dyna-Q+ Exploration Bonus
> Dyna-Q+ extends Dyna-Q for non-stationary environments. For each simulated transition, the reward is augmented: $r + \kappa\sqrt{\tau}$, where $\tau$ is the number of real time steps elapsed since $(s,a)$ was last tried and $\kappa$ is a small constant. This bonus incentivises re-exploration of long-untried state–action pairs, allowing the agent to detect and adapt to changes in the environment (e.g. a shortcut maze that opens mid-episode).

## Significance

Dyna-Q demonstrates that $n$ planning steps can dramatically reduce the number of real environment interactions needed to find a good policy. It is the simplest model that unifies direct RL, model learning, and planning in a single coherent loop, making it the pedagogical reference point for model-based RL.
