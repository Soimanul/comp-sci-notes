**Tags:** #concept #computer-vision #signal-processing
**Related:** [[Fourier Transform (Concept)]], [[Discrete Fourier Transform]], [[Frequency Domain Filtering]], [[Fourier Transform]]

## Definition
The 2D Fourier transform extends the 1D transform to images. The basis functions become 2D complex sinusoids (plane waves), and each pixel in the Fourier spectrum encodes a spatial frequency in both horizontal and vertical directions.

## Formula (2D DFT)

$$F(u, v) = \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x, y) \cdot e^{-i 2\pi (ux/M + vy/N)}$$

## Key Properties of the 2D Spectrum
- **1 pixel in Fourier space** encodes information from **all** pixels in the real image (global basis functions)
- **Each pixel in the Fourier spectrum** is a complex number; we typically visualise only the magnitude $|F(u,v)|$
- **Low frequencies** (near the centre of the spectrum): slow spatial variations, large uniform regions
- **High frequencies** (near the edges): fine detail, sharp edges, noise
- After `fftshift`, DC component is at the centre of the image

## In Python
```python
from numpy.fft import fft2, ifft2, fftshift, ifftshift

F = fftshift(fft2(image))     # compute and centre the spectrum
magnitude = np.log(1 + np.abs(F))  # log scale for visualisation
image_rec = np.real(ifft2(ifftshift(F)))  # reconstruct
```

## Significance
The 2D Fourier transform is the foundation of all frequency-domain operations on images: filtering, the convolution theorem, image resizing in frequency space, and deconvolution.
