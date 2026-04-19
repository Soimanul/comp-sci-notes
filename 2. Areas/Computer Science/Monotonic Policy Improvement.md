**Tags:** #concept #rl
**Related:** [[Trust Region Policy Optimization]], [[Natural Policy Gradient]], [[KL Divergence Constraint in RL]], [[Research Papers and Innovation Trends A]]

## Definition

Monotonic Policy Improvement is a theoretical property stating that a policy update is guaranteed never to decrease the expected return, provided the policy does not deviate too far from the old policy as measured by KL divergence. It provides the theoretical justification for the trust region constraint in TRPO.

> [!info] Key Intuition
> If you can prove that each update step cannot make things worse in expectation, then you have a safe optimization procedure — monotonic improvement means the cumulative return is a non-decreasing sequence under the algorithm.

## The Bound

The key result (Kakade & Langford, 2002; Schulman et al., 2015) states that the expected return of the new policy $\pi_{\theta}$ relative to the old policy $\pi_{\theta_\text{old}}$ satisfies:

$$J(\pi_\theta) \geq J(\pi_{\theta_\text{old}}) + \mathcal{L}_{\theta_\text{old}}(\pi_\theta) - C \cdot \max_s D_\text{KL}(\pi_{\theta_\text{old}}(\cdot|s) \| \pi_\theta(\cdot|s))$$

where $\mathcal{L}_{\theta_\text{old}}(\pi_\theta)$ is a surrogate objective (the importance-weighted advantage sum) and $C$ is a constant. The right-hand side is a lower bound on the true improvement; maximizing this lower bound while keeping $D_\text{KL}$ small guarantees non-negative improvement in $J$.

TRPO operationalizes this by making the KL term a hard constraint:

$$\text{maximize} \quad \mathcal{L}_{\theta_\text{old}}(\pi_\theta) \quad \text{subject to} \quad \mathbb{E}_s\left[D_\text{KL}(\pi_{\theta_\text{old}} \| \pi_\theta)\right] \leq \delta$$

> [!warning] Common Misconception
> Monotonic improvement is a guarantee only in the tabular or linear function approximation setting under the exact bound. With neural networks, TRPO uses an approximation of the bound, so in practice violations can occur — the theory provides strong guidance but not an iron guarantee for deep RL.

## Significance

Monotonic policy improvement is the formal justification for why trust region methods work. Without this theorem, there is no principled reason why constraining the KL divergence should help. It also explains why purely unconstrained gradient ascent on policy parameters is unsafe: there is no bound that prevents the update from collapsing the policy.
