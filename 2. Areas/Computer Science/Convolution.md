**Tags:** #concept #computer-vision #signal-processing
**Related:** [[Linear Shift Invariant System]], [[Cross-Correlation]], [[Gaussian Filter]], [[Convolution Theorem]]

## Definition
Convolution is the mathematical operation at the heart of all linear image filters. In 1D, it computes the integral of the product of two functions after one is reflected and shifted. In 2D discrete form (for images), it sums weighted pixel neighbourhoods.

## 1D Discrete Convolution

$$(f * h)[n] = \sum_{k} f[k] \cdot h[n - k]$$

Note the **flip**: $h$ is reflected before sliding over $f$.

## 2D Discrete Convolution (Images)

$$(f * h)[x, y] = \sum_{m} \sum_{n} f[m, n] \cdot h[x - m,\, y - n]$$

## Key Properties
- **Commutativity**: $f * h = h * f$
- **Associativity**: $(f * g) * h = f * (g * h)$
- **Distributivity**: $f * (g + h) = f*g + f*h$
- **Identity**: $f * \delta = f$ (convolving with the Dirac delta returns the original)

## Convolution vs Cross-Correlation
Cross-correlation does **not** flip the kernel:
$$(f \star h)[x,y] = \sum f[m,n] \cdot h[x+m,\, y+n]$$
For symmetric kernels (e.g., Gaussian), convolution and cross-correlation are identical.

## Border Problem
Near image edges, the kernel extends beyond the image. Solutions: zero-padding, reflection, replication, or ignoring borders.

## Significance
Convolution is the fundamental primitive of image processing. Every linear filter (blur, sharpen, edge detect) is a convolution, and GPUs are optimised for it.
