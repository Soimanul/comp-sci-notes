**Tags:** #concept #computer-vision
**Related:** [[Image Sensors]], [[Aliasing]], [[Sensor Noise]]

## Definition
Pixel size is the physical dimension of a single photodetector on a sensor. Resolution refers to the number of pixels in an image. They are related but distinct properties.

## Key Relationship
Smaller pixels → more pixels per unit sensor area → higher spatial resolution *in principle*. However:
- Smaller pixels collect fewer photons → **lower SNR** (noisier images in low light)
- Below a certain size, diffraction limits the optical resolution regardless of pixel count

A megapixel (MP) = 10⁶ pixels.

## Aliasing
When pixel size is too large relative to the finest detail in the scene, **aliasing** occurs: high-frequency scene content appears as false low-frequency patterns. This is a spatial sampling problem governed by the [[Nyquist Theorem]].

Anti-aliasing filters (optical low-pass filters) placed in front of the sensor prevent this by blurring fine detail before it reaches the pixels.

## Significance
Sensor resolution design is a trade-off between spatial resolution, noise, and cost. For a given optic, there is an optimal pixel size beyond which more pixels add no information.
