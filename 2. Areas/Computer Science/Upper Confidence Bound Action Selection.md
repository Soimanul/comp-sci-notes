**Tags:** #concept #rl
**Related:** [[k-Armed Bandit Problem]], [[Exploration-Exploitation Tradeoff]], [[Epsilon-Greedy Action Selection]]

## Definition

UCB (Upper Confidence Bound) selects actions based on the sum of current value estimate and a confidence interval bonus that decreases as an arm is sampled more:

$$A_t = \arg\max_a \left[ Q_t(a) + c\sqrt{\frac{\ln t}{N_t(a)}} \right]$$

where $N_t(a)$ is the number of times action $a$ has been selected and $c > 0$ controls exploration.

> [!info] Key Intuition
> UCB applies the **optimism in the face of uncertainty** principle: treat unknown arms as potentially optimal until proven otherwise. The bonus term is small for well-sampled arms and large for rarely-tried ones.

## How the Bonus Works

- $c\sqrt{\ln t / N_t(a)}$ grows with time $t$ (we become more curious over time) but shrinks with $N_t(a)$ (once an arm is sampled, uncertainty falls)
- An arm that hasn't been tried in a while accumulates a growing bonus until it is selected again
- Each selection reduces the bonus; the arm is then left alone until uncertainty grows again

## UCB vs ε-Greedy

| | ε-greedy | UCB |
|---|---|---|
| Exploration target | Random | Uncertainty-guided |
| Wasted explorations | Yes (known-bad arms) | No (only uncertain arms) |
| Parameter | ε | c |
| Performance (stationary) | Good | Better |
| Non-stationary | Needs tuning | Harder to adapt |

> [!example]- Worked Example
> At $t=100$: arm 5 has $Q=1.2$, $N=50$; arm 8 has $Q=0.9$, $N=3$; $c=2$. Bonuses: arm 5 = $2\sqrt{\ln 100/50} = 2\sqrt{0.092} \approx 0.61$, total = 1.81; arm 8 = $2\sqrt{\ln 100/3} = 2\sqrt{1.535} \approx 2.48$, total = 3.38. Agent selects arm 8 despite lower estimate.

> [!warning] Common Misconception
> UCB is not guaranteed to be better than ε-greedy in all settings. For non-stationary problems, the $\ln t$ numerator keeps growing, making the algorithm increasingly exploratory — this can be counterproductive.

## Significance

UCB formalises a principled approach to exploration that achieves near-optimal regret bounds ($O(\ln T)$) for stationary bandits, making it the gold standard for bandit exploration strategies.
