**Tags:** #concept #computer-vision
**Related:** [[Bilateral Filter]], [[Sensor Noise]], [[Nonlinear Filters & Morphological Operations]]

## Definition
The median filter is a nonlinear filter that replaces each pixel with the **median** value of the pixels in its neighbourhood. It is highly effective at removing impulsive noise (salt-and-pepper) without blurring edges.

## Why Median, Not Mean?
Salt-and-pepper noise consists of isolated pixels with extreme values (0 or 255). Averaging spreads these extreme values into the neighbourhood. The median is **robust to outliers** — one extreme value cannot shift the median significantly.

## Effect on Salt-and-Pepper Noise
A white (salt) or black (pepper) pixel is replaced by the median of its neighbours, which is typically a non-extreme value → noise removed.

```python
from scipy.ndimage import median_filter
result = median_filter(noisy_img, size=3)
result_cv = cv2.medianBlur(noisy_img_uint8, 3)  # ksize must be odd
```

## Comparison with Gaussian Filter
| | Gaussian | Median |
|---|---|---|
| Outlier removal | No | Yes |
| Edge preservation | Poor | Good |
| Computational cost | Lower | Higher |
| Noise model | Gaussian | Impulsive |

## Significance
The median filter is the standard solution for salt-and-pepper noise and is used wherever impulsive noise is expected (camera transmission errors, sensor defects).
