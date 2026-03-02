**Tags:** #concept #computer-vision
**Related:** [[Template Matching]], [[Gaussian Filter]], [[Aliasing]], [[Convolution & Local Filters]]

## Definition
An image pyramid is a multi-scale representation of an image consisting of a sequence of progressively downsampled (and optionally blurred) versions at halved resolutions.

## Types

### Gaussian Pyramid (most common)
- Level 0: original image
- Level $k$: blur level $k-1$ with a Gaussian, then downsample by 2
- Blurring before downsampling prevents [[Aliasing]]

```python
down = cv2.pyrDown(image)   # blur + halve resolution
up   = cv2.pyrUp(image)     # double resolution (via interpolation)
```

### Laplacian Pyramid
- Difference between adjacent Gaussian pyramid levels
- Captures **band-limited** detail at each scale
- Used in multi-scale blending (panorama stitching)

## Why It's Needed
Many objects appear at different sizes in images. Template matching (or feature detection) at a single scale misses objects that are larger or smaller than the template. Running the algorithm at each pyramid level provides scale invariance.

## Significance
Image pyramids are fundamental to multi-scale analysis in computer vision. They underlie scale-invariant feature detection (SIFT, ORB), optical flow estimation, and efficient coarse-to-fine search strategies.
