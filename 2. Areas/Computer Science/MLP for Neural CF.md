**Tags:** #concept #reco #dl
**Related:** [[Neural Collaborative Filtering]], [[Generalized Matrix Factorization (GMF)]]

## Definition

**MLP for Neural CF** is the non-linear component of NCF that concatenates user and item embeddings and passes them through a stack of fully connected layers with non-linear activations, enabling the model to learn complex interaction patterns beyond the inner product.

> [!info] Key Intuition
> The GMF element-wise product fixes the interaction structure (each user-latent-dimension pairs with the corresponding item-latent-dimension). The MLP concatenation discards that structure and lets the network learn any interaction between any combination of user and item embedding dimensions.

## Architecture

```
User ID  →  User Embedding  $p_u^{MLP}$ ─┐
                                            ├── concat → FC₁ → ReLU → FC₂ → ReLU → ... → FC_L
Item ID  →  Item Embedding  $q_i^{MLP}$ ─┘
```

$$\phi^{MLP}(u, i) = f_L\left(\ldots f_2\left(f_1\left(\begin{bmatrix} p_u^{MLP} \\ q_i^{MLP} \end{bmatrix}\right)\right)\ldots\right)$$

where each $f_l(x) = \text{ReLU}(W_l x + b_l)$.

## Tower Architecture

Typical tower architecture halves the layer width at each level:

| Layer | Input size | Output size |
|---|---|---|
| Input | $2 \times k$ | $2 \times k$ |
| FC₁ | $2k$ | $k$ |
| FC₂ | $k$ | $k/2$ |
| FC₃ | $k/2$ | $k/4$ |

This forces the network to compress the interaction into increasingly abstract representations.

## Why Concatenate Rather Than Element-Wise?

- **Element-wise product** (GMF): only captures dimension-matched interactions ($p_1 \times q_1$, $p_2 \times q_2$, ...)
- **Concatenation** (MLP): the FC layer can mix any user dimension with any item dimension, learning arbitrary cross-dimensional interactions

## Role in NeuMF

The MLP path provides the **non-linear interaction** in NeuMF. Its output $\phi^{MLP}$ is concatenated with $\phi^{GMF}$ before the final prediction layer.

## Significance

The MLP component enables NCF to capture interaction patterns that linear models fundamentally cannot, while the shared embedding layer ensures the user and item representations are learned in a unified space.
