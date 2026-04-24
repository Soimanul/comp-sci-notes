**Tags:** #concept #reco #dl
**Related:** [[Sequential vs Session-Based Recommendation]], [[GRU for Recommendations]], [[Transformer for Sequential Recommendations]]

## Definition

**LSTM for Recommendations** applies Long Short-Term Memory networks to sequential recommendation, using the cell state as long-term memory and the hidden state as working memory for predicting the next user interaction.

> [!info] Key Intuition
> LSTM's explicit cell state allows it to carry information across long interaction sequences without the vanishing gradient problem of vanilla RNNs. This makes it suitable when a user's long-term preferences (from many months of history) must be combined with recent behaviour.

## LSTM Equations

$$f_t = \sigma(W_f [h_{t-1}, x_t] + b_f) \quad \text{(forget gate)}$$
$$i_t = \sigma(W_i [h_{t-1}, x_t] + b_i) \quad \text{(input gate)}$$
$$\tilde{C}_t = \tanh(W_C [h_{t-1}, x_t] + b_C) \quad \text{(candidate cell)}$$
$$C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t \quad \text{(cell update)}$$
$$o_t = \sigma(W_o [h_{t-1}, x_t] + b_o) \quad \text{(output gate)}$$
$$h_t = o_t \odot \tanh(C_t)$$

## Recommendation Use

LSTMs are applied in scenarios where explicit long-term user memory is useful:
- **HRNN** (Hierarchical RNN): two LSTMs — one for within-session dynamics, one for cross-session user state
- Used in music/video streaming where long histories exist

## LSTM vs. GRU for Recommendations

| Aspect | LSTM | GRU |
|---|---|---|
| Gates | 3 (input, forget, output) | 2 (update, reset) |
| Cell state | Explicit separate memory | Merged into hidden state |
| Parameter count | ~33% more than GRU | Less |
| Long-term memory | Explicit via cell state | Implicit in hidden state |
| Practical performance | Similar to GRU | Similar to LSTM |

> [!warning] Preferred Alternative
> In practice, GRU is more commonly used than LSTM in recommendation research because it achieves comparable results with fewer parameters and faster training. Transformer-based models (SASRec) now outperform both in most benchmarks.

## Significance

LSTMs demonstrated that explicit memory mechanisms benefit sequential recommendation, especially for long history modelling. They laid the groundwork for more advanced architectures like HRNN and attention-based sequential models.
