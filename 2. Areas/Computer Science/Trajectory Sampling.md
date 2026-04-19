**Tags:** #concept #rl
**Related:** [[Learning and Planning]], [[Dyna Architecture]], [[Prioritized Sweeping]], [[Dynamic Programming for RL]]

## Definition

Trajectory sampling is a planning strategy in which updates are distributed according to the **on-policy distribution** — the distribution of states and state–action pairs encountered when following the current policy. The agent simulates explicit trajectories through the model and performs backups at each visited state or state–action pair along the way.

> [!info] Key Intuition
> Instead of sweeping every state equally, just simulate trajectories the policy would actually take. States that are unreachable under the current policy are never updated, so computation concentrates exactly where it matters.

## Approaches to Update Distribution

Three approaches exist for deciding which states to update during planning:

1. **Exhaustive sweeps (DP)**: update every $(s,a)$ once per sweep. Infeasible for large state spaces — may not complete even one full sweep before the policy changes.
2. **Uniform random sampling**: sample $(s,a)$ uniformly. Avoids the sweep-completion problem but wastes effort on irrelevant states.
3. **On-policy trajectory sampling** (the recommended approach): simulate full or partial episodes by following the current policy through the model, updating states as they are visited. Naturally concentrates computation on relevant states.

The on-policy distribution partitions states into:
- **Start states** — always updated.
- **Relevant states** — reachable from a start state under some optimal policy; frequently updated.
- **Irrelevant states** — unreachable from any start state under any optimal policy; never updated.

## Real-Time Dynamic Programming (RTDP)

A notable special case is **Real-Time Dynamic Programming (RTDP)**, an on-policy trajectory-sampling version of the value-iteration algorithm. RTDP updates the values of states visited in actual or simulated trajectories using expected (tabular) value-iteration backups. Because it is an asynchronous DP algorithm, updates proceed in the order states are encountered rather than in systematic sweeps, allowing it to skip irrelevant states entirely.

> [!example]- Short vs. Long Runs
> Empirical results on large state spaces show that trajectory sampling with on-policy distribution outperforms uniform random sampling early in learning (because it focuses on reachable states), but the advantage diminishes over time as uniform sampling eventually covers the relevant states too.

## Significance

Trajectory sampling provides a principled way to focus planning computation on states that matter for actual performance, which is especially beneficial with function approximation and in problems with large or continuous state spaces where exhaustive sweeps are impossible.
