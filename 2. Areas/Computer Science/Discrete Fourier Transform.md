**Tags:** #concept #computer-vision #signal-processing
**Related:** [[Fourier Transform (Concept)]], [[Fast Fourier Transform]], [[2D Fourier Transform]]

## Definition
The Discrete Fourier Transform (DFT) is the sampled, finite-length version of the Fourier transform used in digital signal and image processing. For a signal of $N$ samples, it produces $N$ complex frequency coefficients.

## Formula

**Forward DFT:**
$$X[k] = \sum_{n=0}^{N-1} x[n] \cdot e^{-i 2\pi kn / N}, \quad k = 0, 1, \ldots, N-1$$

**Inverse DFT:**
$$x[n] = \frac{1}{N} \sum_{k=0}^{N-1} X[k] \cdot e^{+i 2\pi kn / N}$$

## Complexity
Naïve DFT: $\mathcal{O}(N^2)$ — two nested loops over $N$ frequencies and $N$ samples.

→ See [[Fast Fourier Transform]] for the $\mathcal{O}(N \log N)$ algorithm.

## Interpretation
- $X[0]$: DC component (sum of all values)
- $X[k]$: how much of frequency $k/N$ cycles per sample is in the signal
- Spectrum is periodic and conjugate symmetric for real inputs

## Implementation (Python)
```python
import numpy as np
X = np.fft.fft(x)          # 1D DFT
x_rec = np.fft.ifft(X)     # inverse
```

## Significance
The DFT is the bridge from continuous Fourier theory to digital computation. Combined with the FFT, it enables frequency-domain filtering, compression (JPEG uses DCT), and spectral analysis.
