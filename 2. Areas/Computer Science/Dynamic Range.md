**Tags:** #concept #computer-vision
**Related:** [[High Dynamic Range Imaging]], [[Sensor Noise]], [[Image Sensors]]

## Definition
Dynamic range is the ratio between the largest non-saturating signal and the smallest detectable signal in an imaging system. It defines how wide a range of brightnesses the sensor can capture simultaneously.

## Camera Response Function
The relationship between scene brightness and image pixel value (the **camera response function**, CRF) is:
- **Monotonic** — brighter scenes → higher values
- **Non-linear** — typically follows an S-curve (gamma-like)

The CRF can be empirically calibrated using a target with known relative reflectances (e.g., a **Macbeth colour chart**). Once known, images can be linearized.

## The Exposure Trade-off
- **Short exposure** → captures bright regions well; dark regions are black (no signal)
- **Long exposure** → captures dark regions well; bright regions saturate (all white)

A single exposure can only capture part of the scene's dynamic range if it exceeds the sensor's capability.

## Significance
Dynamic range limits determine when a camera "fails" in high-contrast scenes. This motivates [[High Dynamic Range Imaging]] techniques.
