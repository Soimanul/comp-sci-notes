**Tags:** #concept #computer-vision
**Related:** [[Image Thresholding]], [[CLAHE]], [[Intensity Transformations]]

## Definition
Adaptive thresholding computes a different threshold for each pixel based on the local neighbourhood statistics, handling images with spatially varying illumination.

## Algorithm (Local Mean Method)
For each pixel $(x, y)$:
1. Compute the local weighted mean intensity in a $k \times k$ neighbourhood (weights can be Gaussian)
2. Threshold: if $I(x,y) > \mu_{\text{local}} - C$ → mark pixel as active (foreground)

```python
result = cv2.adaptiveThreshold(
    gray_img, 255,
    cv2.ADAPTIVE_THRESH_GAUSSIAN_C,
    cv2.THRESH_BINARY,
    blockSize=11,   # neighbourhood size (odd)
    C=2             # constant subtracted from the mean
)
```

## Implementation Equivalence
Local adaptive thresholding can be implemented efficiently as:
1. Compute local mean via **convolution** (box or Gaussian filter)
2. Apply standard threshold relative to the local mean

## Significance
Adaptive thresholding is effective for document binarisation (text on unevenly lit paper) and general segmentation in uncontrolled lighting conditions — situations where global [[Otsu's Method]] fails.
