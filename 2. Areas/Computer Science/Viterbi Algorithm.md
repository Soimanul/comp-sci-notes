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
> 
> Tagset: {NN, VB}, sentence: "He saw ducks" (3 tokens, 2 states). Let's trace the $\delta$ and $\psi$ variables.
> 
> **Assumed Probabilities:**
> 
> - $P(\text{NN} \mid \text{START}) = 1.0$
>     
> - $P(\text{VB} \mid \text{NN}) = 0.8$, $P(\text{NN} \mid \text{NN}) = 0.2$
>     
> - $P(\text{NN} \mid \text{VB}) = 0.8$, $P(\text{VB} \mid \text{VB}) = 0.2$
>     
> - $w_2$ "saw": $P(\text{saw} \mid \text{VB}) = 0.9$, $P(\text{saw} \mid \text{NN}) = 0.1$
>     
> - $w_3$ "ducks": $P(\text{ducks} \mid \text{NN}) = 0.8$, $P(\text{ducks} \mid \text{VB}) = 0.2$
>     
> 
> **Step 1: Initialisation ($w_1 = \text{"He"}$)**
> 
> - $\delta_1(\text{NN}) = 1.0 \cdot 1.0 = 1.0$ _(Assuming "He" is unequivocally a Noun here)_
>     
> - $\delta_1(\text{VB}) = 0$
>     
> 
> **Step 2: Recursion ($w_2 = \text{"saw"}$)**
> 
> - **To NN:** $\delta_2(\text{NN}) = \max [1.0 \cdot 0.2] \cdot 0.1 = 0.02$
>     
>     - $\psi_2(\text{NN}) = \text{NN}$
>         
> - **To VB:** $\delta_2(\text{VB}) = \max [1.0 \cdot 0.8] \cdot 0.9 = 0.72$
>     
>     - $\psi_2(\text{VB}) = \text{NN}$
>         
> 
> **Step 3: Recursion ($w_3 = \text{"ducks"}$)**
> 
> - **To NN:** We check previous paths $\left(\delta_2(t') \cdot P(\text{NN} \mid t')\right)$:
>     
>     - From NN: $0.02 \cdot 0.2 = 0.004$
>         
>     - From VB: $0.72 \cdot 0.8 = 0.576 \leftarrow \textbf{Max!}$
>         
>     - $\delta_3(\text{NN}) = 0.576 \cdot 0.8 (\text{emission}) = 0.4608$
>         
>     - $\psi_3(\text{NN}) = \text{VB}$
>         
> - **To VB:** We check previous paths $\left(\delta_2(t') \cdot P(\text{VB} \mid t')\right)$:
>     
>     - From NN: $0.02 \cdot 0.8 = 0.016$
>         
>     - From VB: $0.72 \cdot 0.2 = 0.144 \leftarrow \textbf{Max!}$
>         
>     - $\delta_3(\text{VB}) = 0.144 \cdot 0.2 (\text{emission}) = 0.0288$
>         
>     - $\psi_3(\text{VB}) = \text{VB}$
>         
> 
> **Termination & Backtrack:**
> 
> - $\hat{t}_3 = \arg\max(0.4608, 0.0288) = \textbf{NN}$
>     
> - Backtrack: $\psi_3(\text{NN}) = \textbf{VB} \rightarrow \psi_2(\text{VB}) = \textbf{NN}$
>     
> - Final Sequence: **NN $\rightarrow$ VB $\rightarrow$ NN**
>     

> [!warning] Common Misconception
> Viterbi finds the single best complete sequence — it is NOT the same as greedily picking the best tag at each position independently. Greedy tagging can get locked into locally optimal but globally suboptimal choices.
**Tags:** #concept #nlp #pos #sequence-labelling #viterbi