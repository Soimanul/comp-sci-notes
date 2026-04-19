**Tags:** #topic #hub #rl
**Related:** [[Reinforcement Learning]], [[Markov Decision Process]], [[Reinforcement Learning]]

## Overview

Multi-Agent Reinforcement Learning (MARL) extends single-agent RL to settings where multiple learning agents coexist in a shared environment, each motivated by its own reward signal. MARL is formally modeled as Markov games or extensive-form games and is closely connected to game theory — particularly repeated games. Research in MARL evaluates social metrics (cooperation, reciprocity, equity, social influence) alongside algorithmic performance.

> [!abstract]- TL;DR
> MARL studies multiple agents learning simultaneously in a shared environment. The core challenge is non-stationarity: each agent's environment changes as other agents learn, violating the Markov property. Settings range from pure competition (zero-sum) to pure cooperation (identical rewards) to mixed-sum.

## Knowledge Map

### 1. Formal Foundations
- [[Markov Game]]
- [[Markov Decision Process]]

### 2. Cooperation vs. Competition Taxonomy

| Setting | Reward Structure | Examples |
|---|---|---|
| **Pure competition** | Exactly opposite (zero-sum) | Chess, Go, StarCraft 2-player |
| **Pure cooperation** | Identical rewards | Overcooked, multi-robot coordination |
| **Mixed-sum** | Diverging but non-exclusive | Self-driving cars, Among Us, Diplomacy |

The **exploitation–exploitability tradeoff** defines the landscape: Nash equilibrium (cooperation + non-exploitability) vs. full opponent exploitation (competition + high exploitation risk).

### 3. Key Phenomena
- [[Autocurricula]]: emergent stacked learning phases driven by competitive pressure
- **Sequential social dilemmas (SSD)**: multi-step extensions of matrix games (prisoner's dilemma, chicken, stag hunt) introduced 2017; MARL research focuses on inducing cooperative behaviour via reward shaping or environment design
- **Conventions**: in pure cooperation, agents converge to shared coordination strategies not designed by hand

### 4. Information Structures

| Structure | Description | Common in |
|---|---|---|
| **Centralised** | Central controller aggregates joint actions/rewards/observations | Training phase (CTDE) |
| **Decentralised with networking** | Agents share info with neighbours via communication network | Cooperative MARL |
| **Fully decentralised** | No explicit info exchange; local observations may encode global info | Competitive MARL |

### 5. Algorithm Landscape

MARL algorithms lie at the intersection of TD RL, game theory, and direct policy search:

| Task | Algorithm Examples |
|---|---|
| Fully cooperative (static) | JAL, FMQ |
| Fully cooperative (dynamic) | Team-Q, Distributed-Q, OAL |
| Fully competitive | Minimax-Q |
| Mixed (static) | Fictitious Play, WoLF-IGA, GIGA |
| Mixed (dynamic) | Nash-Q, CE-Q, WoLF-PHC |

**Agent awareness** dimension: Independent (coordination-free) → Tracking (coordination-based) → Aware (indirect coordination / opponent-aware).

### 6. Communication in MARL (Comm-MARL)

Designing a Comm-MARL system requires decisions across 9 dimensions: Communication Type, Communication Policy, Communicated Messages, Message Combination, Inner Integration, Communication Constraints, Communication Learning, Training Scheme, and Controlled Goals.

### 7. Case Studies

**Capture the Flag — FTW Agent (DeepMind, 2019)**
Quake III Arena CTF: mixed-sum (cooperate with teammates, compete with opponents). Three innovations:
1. **Population training** — agents learn by playing against diverse teammates and opponents
2. **Internal rewards** — two-tier optimisation: internal reward $r_t$ shaped by game points $\rho_t$ + winning signal; RL learns policy on internal rewards
3. **Fast and slow timescales** — fast RNN (per-step memory) + slow RNN (episode-level planning); sampled latent variable links timescales

**Multi-Agent Hide and Seek (OpenAI, 2019)**
Six emergent strategies and counterstrategies (hiders: box shelter → lock ramps; seekers: ramp break-in → box surf). Self-supervised autocurriculum produced behaviours the environment designers did not anticipate.

**Hanabi Challenge (Bard et al. 2019, arXiv:1902.00506)**
Cooperative card game (2–5 players, imperfect information). Players see others' cards but not their own. Actions: Hint (costs info token), Discard (recovers token), Play (risks life). Max score 25. Requires **theory of mind** — reasoning about beliefs of other agents. State-of-the-art: WTFWThat 24.89 (5P), BAD (Bayesian Action Decoder) 23.92 (2P). Benchmark: Hanabi Learning Environment.

### 8. Tools
- **PettingZoo** (pettingzoo.farama.org): Python library for MARL research; AEC API and Parallel API; environments: Atari, Butterfly, Classic, MPE, SISL.

> [!question]- Common Exam Questions
> - What fundamental property of single-agent RL is violated in MARL, and why?
> - How do pure competition, pure cooperation, and mixed-sum settings differ in reward structure?
> - What is an autocurriculum and in which type of MARL setting does it emerge?
> - What are the three information structures in MARL, and which is most common in cooperative settings?
> - What makes Hanabi a difficult MARL benchmark compared to full-information games?
