**Tags:** #concept #computer-vision
**Related:** [[Convolution]], [[Template Matching]], [[Convolution Theorem]]

## Definition
Cross-correlation measures the similarity between an image and a template (kernel) at each spatial location. Unlike [[Convolution]], the kernel is **not flipped** before sliding.

## Discrete 2D Cross-Correlation

$$(f \star h)[x, y] = \sum_{m,n} f[x+m,\, y+n] \cdot h[m, n]$$

This is equivalent to computing how well the template $h$ matches the image $f$ at every position $(x, y)$.

## Relationship to Convolution
- For symmetric kernels: $f \star h = f * h$
- `cv2.filter2D` computes cross-correlation (not convolution)

## Maximising Cross-Correlation ≡ Minimising Squared Error

$$\|f - h\|^2 = \|f\|^2 - 2(f \star h) + \|h\|^2$$

Finding the peak of cross-correlation is equivalent to finding the best match location.

## Limitations
Cross-correlation is sensitive to:
- Brightness differences → use **normalised cross-correlation**
- Scale differences → use [[Image Pyramid]]
- Rotation → try multiple orientations

## Significance
Cross-correlation is the mathematical foundation of [[Template Matching]] and is also accelerated by the [[Convolution Theorem]] (multiplication in Fourier space).
