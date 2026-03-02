**Tags:** #concept #computer-vision
**Related:** [[Convolution]], [[Linear Shift Invariant System]], [[Template Matching]], [[Convolution & Local Filters]]

## Definition
A Gaussian filter is a linear filter that convolves an image with a 2D Gaussian kernel. It is the preferred smoothing filter because it has optimal joint localisation in both spatial and frequency domains.

## Kernel
$$h(x, y) = \frac{1}{2\pi\sigma^2} e^{-\frac{x^2+y^2}{2\sigma^2}}$$

Parameters:
- $\sigma$ — controls the spread (larger $\sigma$ = more blur)
- Kernel size — typically chosen as $6\sigma$ (covers 99.7% of the distribution)

## Why Not a Box Filter?
A box (uniform average) filter has sharp corners in the spatial domain → introduces ringing artefacts. The Gaussian is smooth and has no such issue.

## Separability
The 2D Gaussian is separable into two 1D Gaussians:
$$h(x, y) = h(x) \cdot h(y)$$

This halves the computation: apply a 1D Gaussian horizontally, then vertically.

```python
out_cv = cv2.GaussianBlur(img, (k, k), sigma)
out_sep = cv2.sepFilter2D(img, -1, g1d, g1d)  # equivalent
```

## Significance
Gaussian filtering is ubiquitous: it models optical defocus (via [[Point Spread Function]]), underpins multi-scale analysis (image pyramids), and is the standard pre-processing step before edge detection.
