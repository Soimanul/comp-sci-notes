**Tags:** #concept #computer-vision #signal-processing
**Related:** [[Convolution]], [[2D Fourier Transform]], [[Fast Fourier Transform]], [[Frequency Domain Filtering]], [[Template Matching]]

## Definition
The Convolution Theorem states that convolution in the spatial domain corresponds to **pointwise multiplication** in the frequency domain (and vice versa):

$$\mathcal{F}\{f * g\} = \mathcal{F}\{f\} \cdot \mathcal{F}\{g\}$$
$$f * g = \mathcal{F}^{-1}\{\mathcal{F}\{f\} \cdot \mathcal{F}\{g\}\}$$

## Why It Matters

Spatial convolution has complexity $\mathcal{O}(N^2 K^2)$ for an $N \times N$ image and $K \times K$ kernel. Using the FFT:

1. FFT of image: $\mathcal{O}(N^2 \log N)$
2. FFT of kernel: $\mathcal{O}(N^2 \log N)$
3. Pointwise multiply: $\mathcal{O}(N^2)$
4. Inverse FFT: $\mathcal{O}(N^2 \log N)$

**Total**: $\mathcal{O}(N^2 \log N)$ — independent of kernel size $K$.

For large kernels ($K \gg \log N$), this is dramatically faster.

## Applications
- Accelerating [[Gaussian Filter|large-kernel convolutions]]
- Accelerating [[Template Matching]] (cross-correlation in Fourier space)
- Implementing [[Frequency Domain Filtering]] filters
- **Image shifting** in Fourier space (shift = phase multiplication)

## Significance
The Convolution Theorem is the theoretical bridge between spatial and frequency domain processing. It explains why frequency-domain filters and spatial convolution are two views of the same operation.
