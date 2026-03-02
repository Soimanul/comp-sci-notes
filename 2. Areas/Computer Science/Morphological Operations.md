**Tags:** #concept #computer-vision
**Related:** [[Image Thresholding]], [[Nonlinear Filters & Morphological Operations]]

## Definition
Morphological operations are nonlinear image processing operations that modify the shape of binary (or grayscale) regions based on a local **structuring element**. They are applied iteratively at object boundaries.

## Structuring Element
A binary pattern (kernel) that defines the neighbourhood and shape used for the operation. Common shapes: square, cross, circle (pixelated), diamond.

```python
kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (5, 5))
```

## Core Operations

### Dilation
Expands object boundaries. An output pixel is 1 if **any** image pixel under the structuring element is 1.
- Effects: fills holes, connects nearby objects, expands boundaries
```python
dilated = cv2.dilate(img, kernel, iterations=1)
```

### Erosion
Shrinks object boundaries. An output pixel is 1 only if **all** image pixels under the structuring element are 1.
- Effects: removes thin protrusions, separates touching objects
```python
eroded = cv2.erode(img, kernel, iterations=1)
```

### Opening (Erosion → Dilation)
- Removes small objects (salt noise) while preserving larger shapes
```python
opened = cv2.morphologyEx(img, cv2.MORPH_OPEN, kernel)
```

### Closing (Dilation → Erosion)
- Fills small holes (pepper noise) while preserving shape
```python
closed = cv2.morphologyEx(img, cv2.MORPH_CLOSE, kernel)
```

### Morphological Gradient (Dilation − Erosion)
- Produces the thick boundary/contour of objects
```python
gradient = cv2.morphologyEx(img, cv2.MORPH_GRADIENT, kernel)
```

## Grayscale Extension
For grayscale images: erosion = local **minimum**, dilation = local **maximum** over the structuring element neighbourhood.

## Significance
Morphological operations are used in document processing, medical image segmentation, and binary object analysis to enforce prior knowledge about shape and connectivity.
