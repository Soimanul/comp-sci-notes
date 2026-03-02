**Tags:** #concept #computer-vision #signal-processing
**Related:** [[Discrete Fourier Transform]], [[Convolution Theorem]], [[2D Fourier Transform]]

## Definition
The Fast Fourier Transform (FFT) is a divide-and-conquer algorithm that computes the [[Discrete Fourier Transform]] in $\mathcal{O}(N \log N)$ time instead of the naïve $\mathcal{O}(N^2)$.

## Key Insight
A DFT of size $N$ can be split into two DFTs of size $N/2$ — one for the even-indexed inputs and one for the odd-indexed inputs — and combined:

$$X[k] = X_{\text{even}}[k] + e^{-i2\pi k/N} X_{\text{odd}}[k]$$

This recursion reduces the total operations from $N^2$ multiplications to $\frac{N}{2}\log_2 N$.

## Speed Comparison
| $N$ | DFT ($N^2$) | FFT ($N \log_2 N$) |
|-----|-------------|-------------------|
| 1024 | ~1M | ~10K |
| 1M | ~10¹² | ~20M |

## In Practice
```python
import numpy as np
X = np.fft.fft2(image)         # 2D FFT
X_shifted = np.fft.fftshift(X) # shift DC to center
x_rec = np.fft.ifft2(X)        # inverse FFT
```

## Significance
Without the FFT, frequency-domain filtering of large images would be computationally infeasible. The FFT makes [[Convolution Theorem]] acceleration of large-kernel convolutions practical.
