**Tags:** #concept #rl
**Related:** [[RL Applications]], [[RL Engineering Challenges]], [[Industrial AI]], [[Reinforcement Learning]]

## Definition

**Sim-to-Real Transfer** (sim-to-real) is the process of training an RL policy inside a simulator and then deploying it on real physical hardware, with the goal of maintaining performance despite the gap between simulated and real dynamics.

> [!info] Key Intuition
> In real-world RL — especially robotics — training speed is constrained by the simulator, not the GPU. 16 parallel simulators might compress weeks of real-time interaction into hours of training. Sim-to-real is the engineering discipline that makes that compressed training actually transfer to the physical system.

## Why the Gap Exists

| Source of Gap | Description |
|---|---|
| **Physics approximation** | Rigid-body simulators ignore friction, deformation, fluid effects |
| **Sensor noise** | Real cameras, IMUs, and encoders have noise not modelled in simulation |
| **Actuator dynamics** | Real motors have latency, backlash, and wear that simulators omit |
| **Environmental variability** | Real environments have lighting changes, obstacle variation, and human interference |

## Principles for Effective Simulation Design

| Principle | What It Means |
|---|---|
| **Physical meaningfulness** | The simulation must capture the dynamics that matter for the task — not just render correctly but behave correctly |
| **Environmental variability** | Randomise lighting, friction, object positions, and sensor noise during training (domain randomisation) so the policy is robust to the real world's variability |
| **Agent state transfer** | Define the observation space to use quantities that can be measured equivalently in sim and real (e.g. joint angles, not pixel-perfect renders) |
| **Online vs deferred learning** | Decide whether the agent continues learning after deployment (online) or is frozen (deferred); online is more adaptive but riskier in safety-critical settings |

## Scalability Insight

In practice, deep RL training for robotics is **constrained by simulation throughput**, not by deep learning computation. A single simulator running at real-time speed is the bottleneck. Running 16 parallel simulator instances can compress weeks of experience into hours of wall-clock training time — making parallelism a first-class engineering concern.

> [!example]- Domain Randomisation for Robotic Grasping
> To train a robotic gripper to pick up objects of varying shape and mass, the simulator randomises: object size (±20%), surface friction (0.1–0.9), lighting direction, and camera position at each episode reset. The trained policy transfers to real hardware with minimal fine-tuning because it has never seen a fixed simulation — it has learned a policy robust to variation.

> [!warning] Common Misconception
> A visually realistic simulator is not necessarily a good training environment. Physics fidelity matters more than rendering quality for most robotic control tasks. A low-fidelity MuJoCo simulation with domain randomisation often transfers better than a photorealistic simulator with fixed dynamics.

## Significance

Sim-to-real transfer is the central engineering bottleneck for deploying RL in robotics, autonomous vehicles, and Industrial AI. Progress in fast, parallelisable simulation (Isaac Gym, MuJoCo MJX) is as important to the field as progress in RL algorithms.
