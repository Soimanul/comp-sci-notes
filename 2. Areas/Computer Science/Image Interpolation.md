**Tags:** #concept #computer-vision
**Related:** [[Demosaicing]], [[Geometric Transformations]], [[Image Warping]]

## Definition
Image interpolation estimates pixel values at continuous (non-integer) coordinates by using the known discrete pixel grid. It is required whenever an image must be sampled at positions that do not align with pixel centres.

## When It Is Used
- Resizing (zoom in/out)
- Geometric transformation (rotation, warping, distortion correction)
- Demosaicing (recovering missing colour channels)
- Subpixel image shifting

## Methods

### Nearest Neighbour
Assigns the value of the closest pixel. Fast, but produces blockiness.

### Linear / Bilinear
- **1D linear**: weighted average of the two nearest samples based on fractional distance
  $$f(x) = (1 - \alpha) f(\lfloor x \rfloor) + \alpha f(\lceil x \rceil), \quad \alpha = x - \lfloor x \rfloor$$
- **Bilinear (2D)**: apply 1D linear interpolation first along $x$, then along $y$

### Bicubic
Fits a cubic polynomial to the 4 nearest samples in each dimension. Smoother than bilinear; used by default in most image editors.

### Trilinear
Bilinear extended to 3D — e.g., for volumetric data or image pyramids.

## Significance
The choice of interpolation method introduces a trade-off between computation cost and quality. Nearest neighbour is used in speed-critical paths; bicubic is preferred for display and print.
