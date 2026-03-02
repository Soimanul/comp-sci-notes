**Tags:** #concept #computer-vision
**Related:** [[Linear Shift Invariant System]], [[Convolution]], [[Deconvolution]]

## Definition
The Point Spread Function (PSF) is the response of an optical system (lens, microscope) to a point source of light. It characterises all the blur introduced by the imaging system.

## Why It Matters
Optical systems behave as [[Linear Shift Invariant System|LSI systems]]. Therefore, any input image $f$ is blurred by the PSF $h$ through convolution:

$$g = f * h + \text{noise}$$

where $g$ is the observed (blurry) image.

## Measuring the PSF
Image a point source (e.g., a star or a pinhole) through the optical system. The recorded blurry image IS the PSF.

## Implications
- **Forward problem**: Given $f$ and $h$, compute $g$ (simulate blur)
- **Inverse problem**: Given $g$ and $h$, recover $f$ — this is **deconvolution** (see [[Deconvolution]])

## Common PSF Shapes
- **Gaussian**: models diffraction-limited optics and defocus
- **Disc**: ideal out-of-focus blur
- **Motion blur**: linear streak in direction of motion

## Significance
Knowing the PSF enables deblurring (restoring a sharp image from a blurry one). This is critical in astronomy, microscopy, and medical imaging.
