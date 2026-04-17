**Tags:** #hub #rl
**Related:** [[RL Basic Concepts]], [[Bellman Equation]], [[Bellman Optimality Equation]], [[Dynamic Programming]]

## Overview

Dynamic Programming (DP) in RL refers to a collection of algorithms that use a perfect model of the MDP to compute optimal policies. DP performs **full backups** (averaging over all possible transitions) and is the theoretical precursor of all RL methods. The key algorithms — Policy Evaluation, Policy Iteration, and Value Iteration — all exploit the Bellman equations as iterative update operators.

> [!abstract]- TL;DR
> DP requires a perfect model and is computationally expensive but exact. Policy Iteration alternates evaluation and greedy improvement until stable. Value Iteration truncates evaluation to one sweep per improvement step. Both converge to $v_*$ and $\pi_*$. Generalised Policy Iteration (GPI) unifies them: any interleaving of evaluation and improvement converges.

## Knowledge Map

### 1. Foundations
- [[Policy Evaluation]]
- [[Policy Improvement Theorem]]

### 2. Algorithms
- [[Policy Iteration]]
- [[Value Iteration]]
- [[Asynchronous Dynamic Programming]]

### 3. Unifying Framework
- [[Generalized Policy Iteration]]

> [!question]- Common Exam Questions
> - Write the iterative policy evaluation update and describe when it terminates.
> - State the Policy Improvement Theorem. What does it guarantee?
> - How does Value Iteration differ from Policy Iteration? What does Value Iteration sacrifice?
> - What is Generalised Policy Iteration and why does it converge to optimality?
> - Why is DP impractical for large MDPs, and what alternatives does this motivate?
