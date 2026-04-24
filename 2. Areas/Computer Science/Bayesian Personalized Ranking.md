**Tags:** #concept #reco
**Related:** [[Pairwise Loss]], [[Matrix Factorization]], [[Implicit Feedback]]

## Definition

**Bayesian Personalised Ranking (BPR)** is a pairwise learning-to-rank framework for implicit feedback that maximises the posterior probability of user preferences by assuming a user prefers interacted items over non-interacted items.

> [!info] Key Intuition
> We don't know whether a user likes unobserved items — but we can assume they prefer items they *did* interact with over ones they *didn't*. BPR formalises this assumption probabilistically and derives a principled optimisation objective.

## Formulation

**Assume:** For user $u$, item $i$ observed, item $j$ unobserved: $u$ prefers $i$ over $j$.

**BPR posterior:**
$$P(\Theta | >_u) \propto P(>_u | \Theta) \cdot P(\Theta)$$

Using a Bernoulli likelihood:
$$P(i >_u j | \Theta) = \sigma(\hat{r}_{uij}) = \sigma(\hat{r}_{ui} - \hat{r}_{uj})$$

## BPR-OPT Objective

Maximise the log posterior over all user-positive-negative triples $D_S = \{(u, i, j)\}$:

$$\text{BPR-OPT} = \sum_{(u,i,j) \in D_S} \ln \sigma(\hat{r}_{ui} - \hat{r}_{uj}) - \lambda \|\Theta\|^2$$

Equivalently, minimise the negative:
$$L = -\sum_{(u,i,j) \in D_S} \ln \sigma(\hat{r}_{ui} - \hat{r}_{uj}) + \lambda \|\Theta\|^2$$

## BPR-MF Update Rule

When the underlying model is Matrix Factorization ($\hat{r}_{ui} = p_u^T q_i$):

$$\frac{\partial \text{BPR-OPT}}{\partial \Theta} \propto -\frac{e^{-\hat{r}_{uij}}}{1+e^{-\hat{r}_{uij}}} \cdot \frac{\partial (\hat{r}_{ui} - \hat{r}_{uj})}{\partial \Theta}$$

Updates for each triple:
$$p_u \leftarrow p_u + \alpha \left(\frac{1}{1+e^{\hat{r}_{uij}}}(q_i - q_j) - \lambda p_u\right)$$
$$q_i \leftarrow q_i + \alpha \left(\frac{1}{1+e^{\hat{r}_{uij}}} p_u - \lambda q_i\right)$$
$$q_j \leftarrow q_j + \alpha \left(-\frac{1}{1+e^{\hat{r}_{uij}}} p_u - \lambda q_j\right)$$

## Sampling

Bootstrap sampling: uniformly draw $(u, i, j)$ triples from $D_S$. Each step updates one triple — analogous to SGD.

> [!example]- Example
> User watched Movie A and Movie B, but not Movie C. BPR trains on triples:
> (User, Movie A, Movie C), (User, Movie A, Movie D), (User, Movie B, Movie C), ...
> It pushes $\hat{r}_{u,A} > \hat{r}_{u,C}$, etc.

## Significance

BPR-MF is the canonical baseline for implicit feedback recommendation. It consistently outperforms pointwise MF on ranking metrics (NDCG, HR@K) despite the simpler assumption, and is available in libraries like Cornac and implicit.
