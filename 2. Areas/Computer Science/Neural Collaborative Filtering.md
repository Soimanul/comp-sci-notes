**Tags:** #concept #reco #dl
**Related:** [[Matrix Factorization]], [[Inner Product Limitation]], [[Generalized Matrix Factorization (GMF)]], [[MLP for Neural CF]]

## Definition

**Neural Collaborative Filtering (NCF)** is a framework that replaces the inner product interaction function of Matrix Factorization with a neural network, enabling it to learn arbitrary non-linear user-item interaction patterns.

> [!info] Key Intuition
> Matrix Factorization uses $\hat{r}_{ui} = p_u^T q_i$. NCF says: why fix the interaction to a dot product? Let the network learn the best interaction function from data. The resulting model can capture complex patterns that the inner product cannot express.

## Architecture

NCF consists of an embedding layer for both users and items, followed by a neural interaction function. There are two variants, combined in **NeuMF**:

```
User ID  →  [User Embedding]  ─┐
                                ├── Neural Interaction → Output
Item ID  →  [Item Embedding]  ─┘
```

Two interaction functions:
- [[Generalized Matrix Factorization (GMF)]]: element-wise product → linear output
- [[MLP for Neural CF]]: concatenation → fully connected layers

## NeuMF (Neural Matrix Factorization)

NeuMF fuses both:

$$\hat{r}_{ui} = \sigma\left(h^T \begin{bmatrix} \phi_{GMF} \\ \phi_{MLP} \end{bmatrix}\right)$$

- Separate embeddings for GMF and MLP paths
- Final layer $h$ learns to weight the two paths

## Training

- **Loss**: Binary cross-entropy (implicit feedback: 1 for observed, 0 for sampled negatives)
- **Negative sampling**: sample $k$ negatives per positive
- **Initialisation of NeuMF**: pre-train GMF and MLP separately, then use their weights to initialise NeuMF

> [!warning] Inner Product Cannot Be Universal
> NCF is motivated by the universal approximation theorem — a deep enough MLP can approximate any continuous function. The inner product is a specific linear function that may not be the best for all datasets.

## Significance

NCF (He et al., 2017) was a landmark paper demonstrating that neural architectures can outperform MF on implicit feedback recommendation. It sparked a wave of deep learning approaches to collaborative filtering.
