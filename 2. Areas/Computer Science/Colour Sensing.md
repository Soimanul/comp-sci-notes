**Tags:** #concept #computer-vision
**Related:** [[Colour Spaces]], [[Demosaicing]], [[Image Sensors]], [[Image Sensing]]

## Definition
Colour sensing describes how the human visual system and cameras encode colour information. Both reduce a full spectral distribution to a small set of numbers by integrating it against a set of sensitivity functions.

## Human Colour Vision
The retina has two types of photoreceptors:
- **Rods** — sensitive to intensity only (luminance, used in low light)
- **Cones** — 3 types (L, M, S), sensitive to different wavelength ranges

The brain computes **three numbers** (R, G, B — or L, M, S) from the full spectrum. This is described by the **tristimulus curves**.

## Metamers
Multiple different physical spectra can produce identical tristimulus values — these are called **metamers**. This is why colour rendering on screens works: the RGB primaries are not the "real" colours, but they produce the same perceptual response.

## Camera Colour Sensing
Cameras mimic trichromatic vision: each pixel is covered by a colour filter (R, G, or B) so only a narrow wavelength band reaches each photodiode. See [[Demosaicing]] for how a full-colour image is recovered.

## Significance
Trichromacy is the biological reason that RGB is sufficient for colour display and capture. All practical colour models (RGB, HSV, CIE XYZ) are projections of the continuous spectrum through this 3D filter.
