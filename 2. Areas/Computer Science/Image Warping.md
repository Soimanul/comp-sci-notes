**Tags:** #concept #computer-vision
**Related:** [[Affine Transformation]], [[Homography]], [[Image Interpolation]], [[Geometric Transformations]]

## Definition
Image warping is the process of geometrically transforming an image by mapping each output pixel location to a corresponding location in the input image and sampling it via interpolation.

## Forward vs Inverse Warping

**Forward mapping**: for each input pixel $(x, y)$, compute where it maps to in the output.
- Problem: output pixel grid may not be uniformly covered → holes and overlap

**Inverse mapping** (preferred): for each output pixel $(u, v)$, compute the corresponding input location $(x, y)$, then sample via interpolation.
- Guarantees a value for every output pixel
- Requires the inverse transformation $T^{-1}$

## Implementation
$$
\text{output}(u, v) = \text{interpolate}(\text{input},\ T^{-1}(u, v))
$$

Any geometric transformation (translation, rotation, scaling, affine, projective) can be applied this way.

## Significance
Inverse warping + interpolation is the standard pipeline for all image geometric transformations: distortion correction, panorama stitching, image registration, and augmented reality.
