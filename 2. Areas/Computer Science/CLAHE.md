**Tags:** #concept #computer-vision
**Related:** [[Histogram Equalization]], [[Adaptive Thresholding]], [[Intensity Transformations]]

## Definition
CLAHE (Contrast Limited Adaptive Histogram Equalisation) is a local variant of histogram equalisation that operates tile-by-tile and clips the histogram to prevent noise amplification.

## How It Works
1. **Divide** the image into small tiles (e.g., 8×8)
2. **Compute** a separate histogram per tile
3. **Clip** histogram bins above a limit $C$ and redistribute the excess counts uniformly — this prevents over-amplification of noise in nearly uniform regions
4. **Equalise** each tile using its clipped histogram
5. **Interpolate** between neighbouring tile mappings (bilinear) to avoid visible tile boundaries

```python
clahe = cv2.createCLAHE(clipLimit=2.0, tileGridSize=(8, 8))
result = clahe.apply(img)
```

## vs Global Histogram Equalisation
| | Global | CLAHE |
|---|---|---|
| Scope | Whole image | Per tile |
| Noise | Can amplify noise | Controlled by clip limit |
| Artefacts | None | Tile boundaries (smoothed) |

## Significance
CLAHE is the standard contrast enhancement method for medical images (chest X-rays, fundus photography) where local contrast matters and noise amplification must be controlled.
