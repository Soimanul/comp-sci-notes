**Tags:** #concept #reco #dl
**Related:** [[Memorization vs Generalization in Reco]], [[Neural Collaborative Filtering]], [[Factorization Machines]]

## Definition

**Wide & Deep** is a jointly trained recommendation model (Google, 2016) that combines a **wide linear model** (for memorisation of specific feature co-occurrences) with a **deep neural network** (for generalisation to unseen feature combinations via embeddings).

> [!info] Key Intuition
> Recommending the app "Tic Tac Toe" to users who searched for "games for kids AND board games" requires memorising that specific co-occurrence. But generaliasing to new users/items requires a deep model. Wide & Deep does both simultaneously with a single joint loss.

## Architecture

```
Sparse features (user history, context)
         ↓
   [Wide Component]                    [Deep Component]
   Linear model:                       Embedding layer
   y = w^T [x, φ(x)] + b              → Dense 1024 → ReLU
                                       → Dense 512  → ReLU
                                       → Dense 256  → ReLU
         ↓                                    ↓
              ──── concat ────
                     ↓
              sigmoid(wide + deep)
```

**Final prediction:**
$$P(y=1|x) = \sigma(w_{\text{wide}}^T [x, \phi(x)] + w_{\text{deep}}^T a^{(L)} + b)$$

## Feature Assignment

| Component | Feature Types | Examples |
|---|---|---|
| Wide | Raw sparse features + cross-product transformations | Installed app × impressed app |
| Deep | Dense embeddings of categorical features | App ID, User demographics, Device |

## Training

Both components are trained **jointly** with backpropagation, using **mini-batch stochastic gradient descent**. Wide uses Follow-The-Regularized-Leader (FTRL); deep uses AdaGrad.

> [!example]- Google Play Deployment
> Wide: user installed app A AND searched for term B → recommend app C
> Deep: app C's embedding is similar to apps user has installed → generalise to new apps

## Significance

Wide & Deep was deployed in Google Play and improved app downloads significantly. It established the **two-tower + combination** pattern that underlies many modern production recommendation architectures (DeepFM, DCN, etc.).
