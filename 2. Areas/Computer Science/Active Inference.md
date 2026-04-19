**Tags:** #concept #rl
**Related:** [[Advanced RL Techniques]], [[World Models]], [[Reinforcement Learning]]

## Definition

Active Inference is a computational framework from neuroscience (Friston et al.) that unifies perception, learning, and action under a single objective: **minimising variational free energy** (equivalently, minimising surprise / prediction error). Unlike RL, which separates reward maximisation from perception, Active Inference treats action as part of inference — agents act to confirm their predictions about the world.

> [!info] Key Intuition
> In RL, the agent acts to *maximise reward*. In Active Inference, the agent acts to *minimise surprise* about the world — which is equivalent to pursuing preferred outcomes when preferences are encoded in the agent's prior beliefs. Action is not separate from perception; it is a way of sampling the world to resolve uncertainty and steer toward outcomes you prefer.

## The Feedback Loop Model

Active Inference operates as a continuous Predict → Compare → Update → Act loop:

$$\text{Belief/Inference} \to \text{Action} \to \text{Observation} \to \text{(update Belief)}$$

The brain (agent) maintains a probabilistic generative model of hidden world states:
- **Perception**: update beliefs by Bayesian inference given new sensations $p(\text{state} | \text{observation})$
- **Learning**: update model parameters to better predict sensations
- **Action**: select actions that minimise expected future prediction error (Expected Free Energy)

## Variational Free Energy

The variational free energy $F$ bounds the surprise (negative log evidence):

$$F = \underbrace{\text{mismatch to sensations}}_{\text{accuracy}} + \underbrace{\text{complexity penalty}}_{\text{Bayesian Occam's razor}}$$

Minimising $F$ simultaneously fits the model to observations (accuracy) while keeping it parsimonious (complexity). The agent's generative model is the best trade-off between explaining sensory data and avoiding over-fitting.

## Active vs Passive Inference

| Mode | Mechanism |
|---|---|
| **Passive (perception)** | Update beliefs to minimise current prediction error |
| **Active (action)** | Select actions to minimise *future* expected prediction error |

Active inference selects actions that will lead to observations that confirm the agent's predictions — either by reducing uncertainty (epistemic value / information gain) or by realising preferred states (pragmatic value / reward).

## Connection to RL

Active Inference subsumes standard RL: preferences over outcomes are encoded in the agent's prior beliefs $p(\text{preferred outcomes})$. Acting to minimise free energy then naturally leads to seeking preferred outcomes, but with an explicit epistemic component — the agent also actively seeks information about the world, not just reward.

The LLM + Active Inference hybrid architecture demonstrates a practical instantiation: LLM provides imagination (hypotheses, candidate plans); Active Inference provides formal planning via Expected Free Energy minimisation; together they form a hybrid agent that combines generative world knowledge with principled uncertainty-driven action selection.

## Physics as Strong Priors

A critical insight for efficient learning: incorporating strong physical priors (object permanence, continuous motion, collision invariants) into the generative model reduces the training data required by orders of magnitude — a model with strong priors achieves low error from very few observations, while a model with weak priors requires far more data to converge to the same accuracy.

> [!example]- Autonomous Driving Under Uncertainty
> A car approaches an intersection where a figure on the pavement might be a plastic bag or a rock. Active Inference: (A) update belief about hidden cause from observation; (B) choose action (slow down, change lanes, angle head) that *maximally resolves uncertainty* while preferring safe outcomes. This unifies epistemic action (look to confirm) with pragmatic action (slow down for safety) in one principled objective.

> [!warning] Common Misconception
> Active Inference does not avoid reward entirely — preferences *are* rewards, just encoded differently. The difference is that Active Inference explicitly models uncertainty and epistemic value: it will take sub-optimal immediate actions to *gather information* that improves long-run performance. Standard RL typically treats information gathering purely instrumentally (if exploration helps reward); Active Inference treats it as intrinsically valuable.

## Significance

Active Inference provides a principled neuroscientific account of intelligent behaviour that goes beyond RL's reward maximisation. Its practical relevance to RL is growing: the architecture motivates world-model-based agents, physics priors, and the integration of LLMs as internal generative models with RL as the action-selection mechanism.
