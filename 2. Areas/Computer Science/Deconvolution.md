**Tags:** #concept #computer-vision #signal-processing
**Related:** [[Point Spread Function]], [[Convolution Theorem]], [[2D Fourier Transform]], [[Fourier Transform Applications]]

## Definition
Deconvolution is the process of recovering the original sharp image $f$ from a blurred observation $g = f * h + n$, given knowledge of the [[Point Spread Function]] $h$. It is the inverse of convolution.

## Naive Inverse Filter
Using the [[Convolution Theorem]]:

$$\hat{F}(\xi) = \frac{G(\xi)}{H(\xi)}$$

$$\hat{f} = \mathcal{F}^{-1}\left\{\frac{G}{H}\right\}$$

**Problem**: where $H(\xi) \approx 0$ (frequencies the lens cannot pass), dividing amplifies noise catastrophically.

## Regularised Deconvolution (Wiener Filter)
Add a regularisation term to prevent noise amplification:

$$\hat{F}(\xi) = \frac{H^*(\xi)}{|H(\xi)|^2 + \lambda} \cdot G(\xi)$$

where $\lambda > 0$ is the regularisation parameter (trades off sharpness vs noise). Small $\lambda$ → sharper but noisier; large $\lambda$ → smoother.

## Example: Motion Blur
If the PSF is known (direction and length of motion), the Wiener filter can deblur motion-blurred images.

## Significance
Deconvolution is the fundamental image restoration technique. It is used in astronomy (Hubble deblurring), microscopy, and medical imaging to recover detail lost to optical limitations.
