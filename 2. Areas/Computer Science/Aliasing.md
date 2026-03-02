**Tags:** #concept #computer-vision
**Related:** [[Pixel Size & Resolution]], [[Nyquist Theorem]], [[Image Interpolation]]

## Definition
Aliasing is a sampling artefact where high-frequency content in a signal appears as spurious low-frequency content after sampling. In images, it manifests as moiré patterns, jagged edges, or false textures.

## Cause
Aliasing occurs when the sampling rate (pixels per unit length) is **less than twice the highest spatial frequency** in the signal — violating the [[Nyquist Theorem]].

## In Images
- Fine textures (high frequency) sampled with large pixels → appears as a coarse, incorrect pattern
- Resizing an image by downsampling without first blurring also causes aliasing

## Prevention
- Apply a **low-pass filter** (blur) before downsampling to remove frequencies above the Nyquist limit
- In cameras: **optical low-pass filters** (OLPF) placed in front of the sensor
- In software: use proper anti-aliasing during resize operations

## Significance
Aliasing is a fundamental constraint of digital signal processing. Ignoring it produces systematic errors that cannot be corrected after the fact.
