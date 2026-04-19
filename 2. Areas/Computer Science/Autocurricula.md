**Tags:** #concept #rl
**Related:** [[Multi-Agent Reinforcement Learning]], [[Curriculum Learning]], [[Intrinsic Rewards]]

## Definition

An autocurriculum is a sequence of emergent learning phases in a multi-agent system in which each agent's policy improvements change the shared environment, forcing other agents to adapt and develop new strategies. The stacked layers of learning — each dependent on the previous — form a curriculum generated automatically by competitive pressure, not by hand.

> [!info] Key Intuition
> When one team learns a strategy, the opposing team must learn a counter-strategy. That counter-strategy in turn forces the first team to adapt again. The environment itself becomes the teacher — generating an open-ended curriculum of escalating difficulty.

## Mechanism

$$\text{Policy improves} \;\to\; \text{Environment changes} \;\to\; \text{Opponents adapt} \;\to\; \text{New learning phase} \;\to\; \cdots$$

The feedback loop produces distinct phases where each phase's premise is the previous phase's solution. Autocurricula are especially pronounced in adversarial settings and link to the **Red Queen hypothesis** in evolutionary biology: coevolution produces an apparent arms race in which both participants evolve "as fast as they can" only to maintain their relative position (Van Valen, 1973, as cited in Brown, 1995).

> [!example]- Multi-Agent Hide and Seek (OpenAI, 2019)
> Hiders vs. seekers in a simulated environment with moveable boxes and ramps:
>
> | Phase | Hiders learn | Seekers learn |
> |---|---|---|
> | 1 | Run away | Chase |
> | 2 | Build box shelter | Use ramp to break in |
> | 3 | Lock ramps | — |
> | 4 | — | Box-surf (exploit game glitch) |
>
> Each level is an emergent phenomenon. Agents discovered the box-surfing exploit — a behaviour the environment designers did not know the environment supported. 6 distinct strategies and counterstrategies emerged in total.

## Autocurricula vs. Curriculum Learning

| | Autocurricula | Curriculum Learning |
|---|---|---|
| **Origin** | Emergent from competitive pressure | Designed by practitioner |
| **Requires** | Multi-agent adversarial setting | Single agent + task sequence |
| **Content** | Unknown in advance | Specified before training |
| **Scaling** | Self-scaling as agents improve | Fixed unless redesigned |

## Significance

Autocurricula explain why adversarial MARL can produce qualitatively more complex behaviours than single-agent RL: the opponent is always calibrated to the current skill level, providing a continuously challenging learning signal. This principle underlies OpenAI's Hide and Seek, DeepMind's Capture the Flag population training, and self-play in AlphaGo/AlphaZero.

> [!warning] Common Misconception
> An autocurriculum is not the same as self-play. Self-play is a training technique (agent plays against copies of itself); an autocurriculum is the emergent multi-phase learning dynamic that can arise from self-play — but also from multi-population adversarial training or any competitive MARL setting.
