**Tags:** #concept #reco #dl
**Related:** [[Sequential vs Session-Based Recommendation]], [[LSTM for Recommendations]], [[Transformer for Sequential Recommendations]]

## Definition

**GRU for Recommendations (GRU4Rec)** applies Gated Recurrent Units to model sequential user interaction histories, using the hidden state as a representation of the user's evolving preference state. It was the first RNN model to demonstrate strong sequential recommendation performance.

> [!info] Key Intuition
> The GRU hidden state $h_t$ serves as a compressed summary of all items the user has interacted with up to time $t$. The recommendation score for a candidate item $i$ is computed from $h_t$ and item embedding $q_i$.

## GRU Equations

$$z_t = \sigma(W_z x_t + U_z h_{t-1} + b_z) \quad \text{(update gate)}$$
$$r_t = \sigma(W_r x_t + U_r h_{t-1} + b_r) \quad \text{(reset gate)}$$
$$\tilde{h}_t = \tanh(W_h x_t + U_h (r_t \odot h_{t-1}) + b_h) \quad \text{(candidate state)}$$
$$h_t = z_t \odot h_{t-1} + (1 - z_t) \odot \tilde{h}_t \quad \text{(new state)}$$

where $x_t$ = item embedding of the $t$-th interaction.

## GRU4Rec Architecture

```
Item₁ → Item₂ → Item₃ → ... → Item_{t-1}
  ↓        ↓        ↓              ↓
 GRU  →   GRU  →  GRU   →  ...  → GRU → h_{t-1} → score candidate items
```

**Prediction:** $\hat{r}_{u,i} = h_{t-1}^T q_i$ or via a feedforward layer.

## Loss Function

GRU4Rec uses **session-parallel mini-batches** and typically a pairwise ranking loss (BPR or Top-1 loss):

$$L_{\text{TOP1}} = \frac{1}{N_s} \sum_{j=1}^{N_s} \sigma(\hat{r}_{uj} - \hat{r}_{ui}) + \sigma(\hat{r}_{uj}^2)$$

## GRU vs. LSTM for Recommendations

| Property | GRU | LSTM |
|---|---|---|
| Gates | 2 (update, reset) | 3 (input, forget, output) |
| Parameters | Fewer | More |
| Speed | Faster | Slower |
| Performance | Comparable | Comparable |
| Preferred in reco | Yes (GRU4Rec) | Less common |

## Significance

GRU4Rec (Hidasi et al., 2015) established that RNNs can model session-based interaction sequences more effectively than traditional CF methods. It remains a strong baseline for sequential recommendation.
