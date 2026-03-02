**Tags:** #concept #computer-vision
**Related:** [[CLAHE]], [[Otsu's Method]], [[Gamma Correction]], [[Intensity Transformations]]

## Definition
Histogram equalisation is an intensity transformation that remaps pixel values so that the output histogram is as flat (uniform) as possible over the full intensity range, maximising image contrast.

## Core Idea
The cumulative distribution function (CDF) of a uniform distribution is a straight line — meaning each intensity value occurs with equal probability. By mapping pixel values through their empirical CDF, any histogram is warped toward uniformity.

$$
T(k) = (L - 1) \cdot \text{CDF}(k) = \frac{(L-1)}{N} \sum_{i=0}^{k} h(i)
$$

where $h(i)$ is the histogram count at intensity $i$ and $N$ is the total pixel count.

```python
equalized = cv2.equalizeHist(img)
```

## Effect
- Dark images: redistribute mass toward higher values (brighter)
- Bright images: redistribute mass toward lower values (darker)
- Mid-range details: spread out for improved visibility

## Limitation
Global equalisation fails when the image has both bright and dark regions — the global histogram mixes them. → See [[CLAHE]].

## Significance
Histogram equalisation is a standard pre-processing step to improve the contrast of poorly exposed images, widely used in medical imaging (X-ray, MRI) and satellite imagery.
