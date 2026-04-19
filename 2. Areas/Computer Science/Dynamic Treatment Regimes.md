**Tags:** #concept #rl
**Related:** [[RL Applications]], [[Reinforcement Learning]], [[Markov Decision Process]]

## Definition

A **Dynamic Treatment Regime (DTR)** is a sequence of decision rules that specify how to adapt medical treatments — drug types, dosages, timing — to an individual patient's evolving medical history and health state. DTRs formalise personalised medicine as a sequential decision problem, making them a natural RL application.

> [!info] Key Intuition
> A DTR is the medical domain's name for an RL policy: at each clinical visit (timestep), the regime observes the patient's current state and prescribes the next action (treatment), aiming to maximise long-term health outcomes (cumulative reward).

## MDP Formulation

| MDP Component | Clinical Equivalent |
|---|---|
| State $s_t$ | Patient's medical history, biomarkers, current condition |
| Action $a_t$ | Treatment choice: drug, dosage, timing, intervention |
| Reward $r_t$ | Health outcome: symptom reduction, biomarker improvement, survival |
| Transition $P(s_{t+1} \mid s_t, a_t)$ | Patient's biological response to treatment |
| Policy $\pi(a_t \mid s_t)$ | The dynamic treatment regime itself |

## Why RL Is Well-Suited

- **Delayed outcomes**: drug effects may take weeks to manifest — RL's long-horizon credit assignment handles this naturally.
- **Individual variation**: different patients respond differently; RL learns patient-specific policies from historical EHR data.
- **Sequential decisions**: treatment is not a one-shot choice; each visit informs the next, matching the MDP structure.

> [!example]- Sepsis Treatment DTR
> In ICU sepsis management, a DTR learned from patient records decides antibiotic type and dosage at each 4-hour interval based on vital signs, lab results, and prior treatment history. RL-learned DTRs have been shown to outperform average clinician decisions in retrospective studies by adapting more aggressively to deteriorating states early.

> [!warning] Common Misconception
> DTRs are not the same as clinical protocols or guidelines. Protocols are static, population-level rules; DTRs are dynamic, individualised policies that change based on the patient's specific observed trajectory.

## Significance

DTRs represent one of the highest-stakes RL application domains. Success requires careful offline evaluation (no live patient experimentation during training), robust uncertainty quantification, and clinical validation before deployment.
