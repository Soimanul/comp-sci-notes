**Tags:** #concept #reco #dl
**Related:** [[CNN for Sequential Recommendations]], [[Sequential vs Session-Based Recommendation]]

## Definition

**Dilated convolutions for sequential recommendations** use convolutional filters with gaps (dilation) between filter taps, allowing the model to capture long-range dependencies in interaction sequences without increasing the filter size or number of parameters.

> [!info] Key Intuition
> A standard CNN with kernel size $k$ can look back $k$ steps. A dilated CNN with dilation rate $d$ inserts $d-1$ zeros between filter taps, allowing the same $k$-tap filter to span $k + (k-1)(d-1)$ timesteps — exponentially larger receptive fields with stacked dilated layers.

## Dilation Rates

With dilation rate $d$ and kernel size $k$, the **receptive field** after $L$ stacked dilated layers with rates $1, 2, 4, \ldots, 2^{L-1}$:

$$\text{Receptive field} = k + (k-1)(2^L - 2) \approx k \cdot 2^L$$

Doubling the dilation rate at each layer gives exponential coverage of the history.

## Dilated Causal Convolution for Sequences

```
Layer 3 (d=4):  ○   ○   ○   ○
                |   |   |   |
Layer 2 (d=2):  ○   ○   ○   ○   ○   ○   ○   ○
                |   |   |   |   |   |   |   |
Layer 1 (d=1):  ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○
```

**Causal masking**: only look at past items (no future leakage). Implemented by padding the input on the left.

## Usage in Recommendations

- **NextItNet**: stacks dilated residual convolutional blocks for session-based recommendation
- Achieves receptive field comparable to RNNs with fewer parameters and fully parallel computation
- Works well for session-based recommendation where long-range dependencies matter

> [!example]- Receptive Field
> Stack 8 layers with dilation rates 1,2,4,8,16,32,64,128 and kernel size 2:
> Receptive field = $2 \cdot 2^8 = 512$ steps — covers hundreds of past interactions.

## Significance

Dilated convolutions solve the tension between parallelism (CNN) and long-range modelling (RNN), making them a practical alternative to LSTMs/GRUs for long interaction sequences while being faster to train.
