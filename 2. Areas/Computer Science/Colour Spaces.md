**Tags:** #concept #computer-vision
**Related:** [[Colour Sensing]], [[Image Sensing]]

## Definition
A colour space is a systematic way to represent colours as tuples of numbers, consisting of a colour model, a reference white point, a gamut (representable subset of colours), and transfer functions (how values map to physical intensities).

## Key Colour Spaces

### LMS / CIE XYZ
- Based on the cone responses of the human eye
- **CIE 1931 XYZ** is a linear projection of LMS corrected for human sensitivity
- Device-independent; used as a reference

### CIE xy Chromaticity Diagram
- A 2D slice of XYZ at constant luminance
- Represents all visible colours; forms the familiar horseshoe shape
- The outer boundary = monochromatic (pure wavelength) colours

### RGB
- Additive model used by displays and cameras
- R, G, B in range $[0, 255]$ (8-bit) or $[0, 1]$
- Device-dependent (sRGB, Adobe RGB differ)

### HSV
- More intuitive than RGB:
  - **Hue** (0–360°): type of colour (wavelength proxy)
  - **Saturation** (0–100): purity (0 = grey, 100 = pure colour)
  - **Value** (0–100): luminance (0 = black, 100 = brightest)
- Useful for colour-based segmentation

## Practical Notes
- Histogram equalisation should be applied only to the V (or L) channel — not to R, G, B independently — to avoid hue shifts
- OpenCV uses **BGR** channel order by default

## Significance
Choosing the right colour space for a task (e.g., HSV for colour segmentation, LAB for perceptual uniformity) can greatly simplify algorithm design.
