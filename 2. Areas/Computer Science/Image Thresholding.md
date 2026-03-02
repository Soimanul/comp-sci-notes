**Tags:** #concept #computer-vision
**Related:** [[Otsu's Method]], [[Adaptive Thresholding]], [[Intensity Transformations]]

## Definition
Thresholding converts a grayscale image into a binary image by mapping pixel values above a threshold $T$ to 1 (white) and values below to 0 (black). It is the simplest form of image segmentation.

## Global Thresholding

$$
\text{output}(x,y) = \begin{cases} 255 & \text{if } I(x,y) > T \\ 0 & \text{otherwise} \end{cases}
$$

```python
bin_img = np.where(gray_img > T, 255, 0)
```

## Limitations of Global Thresholding
A single threshold fails when:
- Illumination varies across the image (shadows, gradients)
- Object and background intensities overlap significantly

→ See [[Adaptive Thresholding]] and [[Otsu's Method]] for solutions.

## When It Works Well
Controlled environments with uniform lighting (e.g., industrial inspection lines) allow global thresholding to produce high-quality segmentation.

## Significance
Despite its simplicity, thresholding is the basis of many binary image operations (morphology, connected components) and remains practical in constrained settings.
