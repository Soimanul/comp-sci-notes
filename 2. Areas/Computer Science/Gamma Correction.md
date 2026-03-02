**Tags:** #concept #computer-vision
**Related:** [[Histogram Equalization]], [[Dynamic Range]], [[Intensity Transformations]]

## Definition
Gamma correction is a power-law intensity transformation that adjusts the perceptual brightness of an image to account for the non-linear response of human vision or to compensate for display gamma.

## Formula

$$
I_{\text{out}} = I_{\text{in}}^\gamma \quad \text{(values normalised to [0, 1])}
$$

| $\gamma$ | Effect |
|---------|--------|
| $< 1$ | Brightens image (pushes histogram toward high values) |
| $> 1$ | Darkens image (pushes histogram toward low values) |
| $= 1$ | Identity (no change) |

## Efficient Implementation (Lookup Table)
```python
table = np.array([((i / 255.0) ** gamma) * 255
                  for i in np.arange(0, 256)]).astype("uint8")
result = cv2.LUT(image, table)
```

## Why It Matters
Human vision has a non-linear response to luminance (we are more sensitive to changes in dark regions). Gamma encoding matches image storage to perceptual uniformity. **sRGB** images use $\gamma \approx 2.2$.

## Significance
Gamma correction is essential when performing linear operations (e.g., convolution, filtering) on images: they must first be **linearised** ($\gamma = 1/2.2$) so that pixel values represent physical light levels.
