**Tags:** #concept #reco
**Related:** [[Inner Product Limitation]], [[Field-Aware Factorization Machines]], [[Matrix Factorization]]

## Definition

**Factorization Machines (FM)** are a supervised learning model that captures pairwise interactions between all features using factorised parameters, making them applicable to any feature-rich prediction task (CTR, rating, ranking).

> [!info] Key Intuition
> Instead of learning a weight for every feature pair (which is quadratic and sparse), FM learns a latent vector $v_i \in \mathbb{R}^k$ for each feature. The interaction between features $i$ and $j$ is approximated by $\langle v_i, v_j \rangle$ — enabling generalisation even for feature pairs never seen together in training.

## Model (Degree 2)

$$\hat{y}(x) = w_0 + \sum_{i=1}^{n} w_i x_i + \sum_{i=1}^{n} \sum_{j=i+1}^{n} \langle v_i, v_j \rangle \, x_i x_j$$

Where:
- $w_0$ = global bias
- $w_i$ = linear weight for feature $i$
- $v_i \in \mathbb{R}^k$ = latent vector for feature $i$
- $\langle v_i, v_j \rangle = \sum_{f=1}^{k} v_{if} v_{jf}$ = dot product interaction

## Efficient Computation

Naïve computation of all pairwise interactions is $O(kn^2)$. Using the identity:

$$\sum_{i=1}^{n} \sum_{j=i+1}^{n} \langle v_i, v_j \rangle x_i x_j = \frac{1}{2} \sum_{f=1}^{k} \left[ \left( \sum_{i=1}^{n} v_{if} x_i \right)^2 - \sum_{i=1}^{n} v_{if}^2 x_i^2 \right]$$

This reduces complexity to **O(kn)** — linear in the number of features.

## Relationship to Matrix Factorization

When the input $x$ is a one-hot encoding of user and item IDs (user indicator + item indicator), FM reduces exactly to standard Matrix Factorization:
- $v_{\text{user}} \cdot v_{\text{item}}$ = latent factor inner product

FM thus **subsumes MF** as a special case while supporting arbitrary additional features.

> [!example]- CTR Prediction
> Features: user_id=Alice, item_id=Movie42, time_of_day=Evening, device=Mobile.
> FM learns pairwise interactions: Alice×Movie42 (personalised preference), Evening×Mobile (context interaction), etc. — all within one model.

## Significance

FM is one of the most practically important recommendation algorithms, combining the simplicity and scalability of linear models with the interaction-modelling power of MF. It is the foundation of DeepFM, xDeepFM, and many other production architectures.
