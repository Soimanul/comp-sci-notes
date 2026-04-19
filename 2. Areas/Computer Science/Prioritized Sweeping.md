**Tags:** #concept #rl
**Related:** [[Learning and Planning]], [[Dyna-Q]], [[Dyna Architecture]], [[Dynamic Programming for RL]]

## Definition

Prioritized sweeping is a model-based planning algorithm that focuses backup computation on state–action pairs whose value estimates would change the most if updated, propagating value information backward from recently changed states rather than sweeping uniformly.

> [!info] Key Intuition
> Don't waste planning steps on states whose values are already accurate. Work backwards from states that just changed — their predecessors are the ones most likely to need updating next.

## Mechanism

A priority queue $\text{PQueue}$ stores state–action pairs ordered by the magnitude of their potential update (the "urgency"):

$$P \leftarrow \left|R + \gamma \max_a Q(S',a) - Q(S,A)\right|$$

If $P > \theta$ (a small threshold), $(S,A)$ is inserted into $\text{PQueue}$ with priority $P$.

**Algorithm (deterministic environment):**

**Initialize** $Q(s,a)$, $\text{Model}(s,a)$, $\text{PQueue}$ (empty).

**Loop forever:**
- (a–d) Take real action, observe $R,S'$, update $\text{Model}(S,A)$
- (e) Compute $P = |R + \gamma\max_a Q(S',a) - Q(S,A)|$; if $P > \theta$, push $(S,A,P)$ to $\text{PQueue}$
- (f) Repeat $n$ times while $\text{PQueue}$ non-empty:
  - Pop highest-priority $(S,A)$; retrieve $R,S' \leftarrow \text{Model}(S,A)$
  - Apply Q-learning backup
  - For all $(\bar{S},\bar{A})$ predicted to lead to $S$:
    - $\bar{R} \leftarrow$ predicted reward; $P \leftarrow |\bar{R} + \gamma\max_a Q(S,a) - Q(\bar{S},\bar{A})|$
    - If $P > \theta$, insert $(\bar{S},\bar{A})$ into $\text{PQueue}$ with priority $P$

> [!example]- Rod Maneuvering Task (Moore & Atkeson, 1993)
> A rod must be navigated around obstacles to a goal in a workspace with 14,400 potential states and 4 actions. Prioritized sweeping finds the shortest solution where uniform (unprioritized) sweeping fails to converge in reasonable time — because prioritization concentrates all updates along the relevant path from start to goal.

> [!warning] Predecessor Tracking Requirement
> Prioritized sweeping requires the model to support **reverse queries**: given a state $S$, which $(\bar{S},\bar{A})$ pairs lead to $S$? This reverse model must be maintained explicitly, adding memory and update overhead compared to standard Dyna-Q.

## Significance

Prioritized sweeping can dramatically reduce the number of planning steps needed to propagate information through a large state space. It generalises the idea of backward induction — working back from goal states — to arbitrary changes in value, making it applicable to any ongoing learning scenario.
