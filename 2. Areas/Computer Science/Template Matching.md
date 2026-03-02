**Tags:** #concept #computer-vision
**Related:** [[Cross-Correlation]], [[Image Pyramid]], [[Convolution & Local Filters]]

## Definition
Template matching finds the location(s) in an image where a given template (small sub-image) best matches, using cross-correlation or a related similarity measure.

## Method
Compute [[Cross-Correlation]] (or a normalised variant) between the image and template at every position. The peak response indicates the best match.

```python
res = cv2.matchTemplate(img, template, cv2.TM_CCOEFF_NORMED)
min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(res)
```

## Similarity Measures
| Method | Property |
|--------|----------|
| `TM_CCORR` | Raw cross-correlation |
| `TM_CCOEFF_NORMED` | Normalised; brightness-invariant |
| `TM_SQDIFF_NORMED` | Squared error; lower = better match |

## Limitations

| Issue | Workaround |
|-------|-----------|
| Brightness sensitive | Use normalised cross-correlation |
| Scale sensitive | Apply at multiple scales via [[Image Pyramid]] |
| Rotation sensitive | Try multiple rotated templates |
| Computationally slow | Accelerate with [[Convolution Theorem]] (FFT) |

## Significance
Template matching is the baseline object detection method. It is widely used in quality inspection, medical image registration, and as a subroutine in more advanced detectors. The [[Convolution Theorem]] makes it feasible for large images and templates.
