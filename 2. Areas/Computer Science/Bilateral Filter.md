**Tags:** #concept #computer-vision
**Related:** [[Gaussian Filter]], [[Median Filter]], [[Nonlinear Filters & Morphological Operations]]

## Definition
A bilateral filter is an edge-preserving smoothing filter that computes a weighted average of the neighbourhood, where weights depend on both **spatial distance** (like a Gaussian) and **intensity similarity**.

## Core Idea
The Gaussian filter averages all neighbouring pixels equally — this smooths edges because pixels on both sides of an edge are averaged together. The bilateral filter avoids this by giving low weight to pixels that differ greatly in intensity.

## Formula

$$I'(x) = \frac{1}{W_p} \sum_{y \in \Omega} I(y) \cdot \underbrace{G_{\sigma_s}(\|x - y\|)}_{\text{spatial}} \cdot \underbrace{G_{\sigma_r}(|I(x) - I(y)|)}_{\text{intensity}}$$

where $W_p$ is a normalisation constant.

Parameters:
- $\sigma_s$ — spatial spread (neighbourhood size)
- $\sigma_r$ — intensity spread (similarity threshold)

```python
result = cv2.bilateralFilter(img, d=9, sigmaColor=75, sigmaSpace=75)
```

## Effect
- Smooth regions: both kernels are large → strong smoothing (like Gaussian)
- Across edges: intensity kernel drops to near zero → edge preserved

## Limitation
Bilateral filtering is **non-linear** and therefore cannot be accelerated via FFT. It is significantly slower than Gaussian filtering.

## Significance
The bilateral filter is the foundation of many advanced filtering techniques (guided image filter, joint bilateral filter) and is used in portrait photography, depth map upsampling, and HDR tone mapping.
