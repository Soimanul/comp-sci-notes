**Tags:** #concept #computer-vision
**Related:** [[Image Thresholding]], [[Histogram Equalization]], [[Intensity Transformations]]

## Definition
Otsu's method is an automatic global thresholding algorithm that selects the threshold $T^*$ which maximises the **between-class variance** of the foreground and background pixel distributions.

## Algorithm
For each candidate threshold $T \in [0, 255]$:
1. Divide pixels into two classes: below $T$ (background) and above $T$ (foreground)
2. Compute the weighted between-class variance:

$$\sigma_B^2(T) = \omega_0 \omega_1 (\mu_0 - \mu_1)^2$$

where $\omega_i$ are class probabilities and $\mu_i$ are class means.

3. Select $T^* = \arg\max_T \sigma_B^2(T)$

```python
thr, out_img = cv2.threshold(gray_img, 0, 255,
                              cv2.THRESH_BINARY + cv2.THRESH_OTSU)
```

## Assumption
Otsu's method assumes the image histogram is bimodal (two clear peaks for foreground and background). It fails on unimodal histograms.

## Significance
Otsu's method eliminates the need to manually select a threshold — a major practical advantage. It is the standard baseline for automatic binarization in document processing and medical imaging.
