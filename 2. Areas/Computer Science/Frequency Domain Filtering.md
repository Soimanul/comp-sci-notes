**Tags:** #concept #computer-vision #signal-processing
**Related:** [[2D Fourier Transform]], [[Convolution Theorem]], [[Fourier Transform Applications]]

## Definition
Frequency domain filtering modifies an image by multiplying its Fourier spectrum by a mask function (the filter's frequency response), then transforming back. This provides direct, intuitive control over which spatial frequencies are retained or removed.

## General Pipeline
1. Compute 2D FFT: $F = \mathcal{F}\{f\}$
2. Multiply by filter mask $H$: $G = H \cdot F$
3. Reconstruct: $g = \mathcal{F}^{-1}\{G\}$

## Types of Filters

### Low-Pass Filter
- **Goal**: keep low frequencies (slow variations), remove high frequencies (fine details, noise)
- **Implementation**: circular mask with 1s in the centre, 0s outside
- **Effect**: smoothing, blurring
- **Caution**: hard binary masks cause ringing artefacts → use soft masks (Gaussian, Butterworth)

### High-Pass Filter
- **Goal**: keep high frequencies, remove low frequencies
- **Implementation**: circular mask with 0s in the centre, 1s outside
- **Effect**: edge enhancement, sharpening; removes gradual illumination changes

### Band-Pass Filter
- **Goal**: keep only a range of frequencies
- **Implementation**: annular mask (ring shape)
- **Effect**: isolates specific scales of texture or structure

## Selecting Mask Size
The cutoff radius relates to feature size: $r \approx 1 / \text{feature\_size}$.

```python
# Low-pass example (Gaussian mask)
H = np.exp(-D2 / (2 * sigma**2))   # D2 = distance squared from centre
G = H * fftshift(fft2(img))
g = np.real(ifft2(ifftshift(G)))
```

## Significance
Frequency domain filtering offers an intuitive way to design filters for specific scales, and is computationally efficient via [[Convolution Theorem]] + [[Fast Fourier Transform]].
