**Tags:** #concept #nlp #pos #sequence-labelling
**Related:** [[HMM-Based POS Tagger]], [[POS Tagging]], [[Markov Assumption]]

## Definition

The Viterbi algorithm is a dynamic programming algorithm that finds the most probable hidden state sequence in an HMM. In POS tagging it finds $\arg\max_{\mathbf{t}} P(\mathbf{w}, \mathbf{t})$ in $O(n \cdot |T|^2)$ time.

> [!info] Key Intuition
> Instead of enumerating all $|T|^n$ tag sequences, Viterbi reuses the best partial path ending at each tag: the best path to position $i$ with tag $t$ is the best path to position $i-1$ over all tags, extended by the transition and emission at $i$.

## Core Mechanics

**Initialisation** ($i = 1$):
$$\delta_1(t) = P(t \mid \text{START}) \cdot P(w_1 \mid t)$$

**Recursion** ($i = 2, \ldots, n$):
$$\delta_i(t) = \max_{t'} \left[\delta_{i-1}(t') \cdot P(t \mid t')\right] \cdot P(w_i \mid t)$$
$$\psi_i(t) = \arg\max_{t'} \left[\delta_{i-1}(t') \cdot P(t \mid t')\right]$$

**Termination**:
$$\hat{t}_n = \arg\max_t \delta_n(t)$$

**Backtrack** via $\psi$ to recover the full tag sequence. Work in log space to avoid underflow.

> [!example]- Worked Example
> Tagset: {NN, VB}, sentence: "fish can fly" (3 tokens, 4 states including START)
> Build a $2 \times 3$ grid of $\delta$ values, fill left-to-right, backtrack the argmax path. Each cell takes constant time: 3 grid cells × 2 transitions = 6 operations per column.

> [!warning] Common Misconception
> Viterbi finds the single best complete sequence — it is NOT the same as greedily picking the best tag at each position independently. Greedy tagging can get locked into locally optimal but globally suboptimal choices.
