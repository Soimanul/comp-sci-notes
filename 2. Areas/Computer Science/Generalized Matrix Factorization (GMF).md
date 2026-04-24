**Tags:** #concept #reco #dl
**Related:** [[Neural Collaborative Filtering]], [[Matrix Factorization]], [[MLP for Neural CF]]

## Definition

**Generalised Matrix Factorization (GMF)** is the linear component of NCF that reformulates standard Matrix Factorization as a neural network with a single linear output layer, enabling integration into the broader NCF framework.

> [!info] Key Intuition
> Standard MF predicts $\hat{r}_{ui} = p_u^T q_i$. GMF replaces the fixed inner product with an element-wise product followed by a learned linear layer: $\hat{r}_{ui} = \sigma(h^T (p_u \odot q_i))$. When $h = \mathbf{1}$ and $\sigma$ is identity, this exactly recovers MF.

## Architecture

```
User ID  →  User Embedding  $p_u^{GMF}$  ─┐
                                             ├── element-wise × → linear → sigmoid
Item ID  →  Item Embedding  $q_i^{GMF}$  ─┘
```

$$\phi^{GMF}(u, i) = p_u^{GMF} \odot q_i^{GMF}$$

$$\hat{r}_{ui} = \sigma(h^T \phi^{GMF})$$

where $\odot$ = element-wise (Hadamard) product and $h \in \mathbb{R}^k$ is a learnable weight vector.

## Relationship to Standard MF

| Setting | Result |
|---|---|
| $h = \mathbf{1}$, linear activation | $\hat{r}_{ui} = \sum_f p_{uf} q_{if} = p_u^T q_i$ (standard MF) |
| Learned $h$, sigmoid | GMF — a more expressive generalisation |

## Role in NeuMF

GMF provides the **linear interaction** path in NeuMF. Its element-wise product maintains the structured interaction between user and item dimensions, complementing the unstructured interaction learned by the MLP path.

## Significance

GMF bridges classic matrix factorization and neural collaborative filtering, providing interpretability (each dimension's contribution is tracked) while allowing the model to learn the optimal weighting of those dimensions.
