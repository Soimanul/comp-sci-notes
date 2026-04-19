**Tags:** #concept #rl
**Related:** [[RL Applications]], [[RL Engineering Challenges]], [[Reinforcement Learning]], [[Curriculum Learning]]

## Definition

A **Concept Network** decomposes a complex RL task into a set of subconcept controllers, each responsible for a simpler subtask. A **selector controller** decides which subconcept controller is active at each timestep, synthesising classical and neural controllers into a unified policy.

> [!info] Key Intuition
> Instead of training one monolithic agent to solve a hard task end-to-end, Concept Networks build a team of specialists — each expert at one piece of the problem — and let a coordinator pick the right expert at each moment. The hard task becomes a set of easy tasks plus an easy selection problem.

## Architecture

```
Selector Controller
├── Subconcept 1: [e.g. Reach]
├── Subconcept 2: [e.g. Orient]
├── Subconcept 3: [e.g. Grasp]
├── Subconcept 4: [e.g. Move]
└── Subconcept 5: [e.g. Stack]
```

Each subconcept can be implemented as a **classical controller** (rule-based, known physics) or a **neural controller** (learned policy), and the selector can mix both kinds.

> [!example]- Bonsai Grasp-and-Stack Robot
> Microsoft Bonsai's grasp-and-stack task decomposes into five subconcepts: Reach (move arm over object), Orient (rotate wrist to grasp angle), Grasp (close gripper), Move (transport to destination), Stack (lower and release). Each is trained separately with a focused reward function. The selector routes between them based on task state. This is far easier to train than a single policy rewarded only on final stack success.

## Advantages

| Advantage | Explanation |
|---|---|
| **Reuse prior knowledge** | Subconcept controllers can be classical (physics-based) where the dynamics are known, eliminating the need to learn from scratch |
| **Modular reward functions** | Each subconcept gets a local, well-specified reward — sidestepping the reward design problem for the composite task |
| **Component replacement** | A poorly performing subconcept can be swapped out or retrained without touching the rest of the network |
| **Interpretability** | The selector's choices are inspectable; you can see which subconcept is active and why |

> [!warning] Common Misconception
> Concept Networks are not hierarchical RL (options framework). The selector does not learn to compose options over sub-episodes; it operates at every timestep and can switch freely. The key innovation is the **explicit representation of subconcepts as named, modular components**.

## Significance

Concept Networks are particularly valuable in industrial and robotics settings where some dynamics are well-understood (classical control) and some are not (grasping under uncertainty). They reduce training complexity and make RL deployments more maintainable.
