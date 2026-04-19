**Tags:** #concept #rl
**Related:** [[RL Applications]], [[Reinforcement Learning]], [[ModelOps]]

## Definition

The analytics hierarchy classifies data-driven systems by the complexity of the question they answer:

| Tier | Question | Technology |
|---|---|---|
| **Descriptive** | What happened? | Reporting, dashboards, BI |
| **Predictive** | What will happen? | Supervised ML, forecasting |
| **Prescriptive** | What should we do? | Optimisation, RL, decision theory |

Reinforcement Learning sits squarely in the **prescriptive** tier: it does not merely forecast an outcome but selects a sequence of actions to maximise a long-term objective.

> [!info] Key Intuition
> Most ML pipelines stop at prediction — they tell you what will happen next. RL closes the loop: it uses that prediction to decide what action to take, observe the result, and improve. This makes RL architecturally different from, not just more advanced than, supervised ML.

## The AI Analytics Cycle

A deployment-ready AI system cycles through:

$$\text{Data} \rightarrow \text{Models} \rightarrow \text{AI Deployment Strategy} \rightarrow \text{Actions} \rightarrow \text{Decisions} \rightarrow \text{Data}$$

RL systems close this cycle explicitly: actions taken by the policy generate new data that feeds back into training. Supervised ML systems do not close this loop — their outputs inform human decisions, which generate data separately.

## ModelOps

**ModelOps** is the operational practice of running this cycle in production:

$$\text{Data Prep} \rightarrow \text{Develop} \rightarrow \text{Deploy} \rightarrow \text{Monitor} \rightarrow \text{Inference} \rightarrow \text{Retrain} \rightarrow \text{Develop} \ldots$$

The ML Dev + Ops infinity loop. For RL, the retrain step is especially important because the environment itself changes as a result of the policy's actions (non-stationarity).

> [!example]- Datacenter Cooling as Prescriptive AI
> A descriptive system would report cooling energy usage. A predictive system would forecast energy usage given planned workloads. DeepMind's DQN-based cooling controller is prescriptive: it observes current temperatures and setpoints, decides on cooling system actions, and adapts in real time to minimise energy while maintaining safety constraints.

> [!warning] Common Misconception
> Prescriptive analytics does not require RL. Linear programming, MIP solvers, and rule-based optimisers are also prescriptive. RL is specifically valuable when the state space is too large for explicit enumeration and when the environment dynamics are unknown or non-stationary.

## Significance

Framing RL as prescriptive analytics helps position it correctly in the AI stack: it is the technology that turns prediction into action, and the one most organisations have not yet deployed. This is why Industrial AI — where the gap between descriptive dashboards and prescriptive control is enormous — represents the next major RL application frontier.
