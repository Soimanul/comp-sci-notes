**Tags:** #concept #computer-vision
**Related:** [[Reflection Mechanisms]], [[Image Sensing]], [[Sensor Noise]]

## Definition
Illumination describes the light sources in a scene that interact with surfaces to produce the brightness seen by the camera. Illumination changes can dominate pixel values and are a major source of computer vision failures.

## Types of Light Sources

| Type | Description | Key Property |
|------|-------------|--------------|
| **Point source** | Rays spread in all directions | Intensity ∝ 1/distance² |
| **Directional source** | Effectively at infinity | Parallel rays, constant intensity |
| **Area source** | Extended emitting region | Soft shadows, hard to model |
| **Ambient** | Scattered indirect light | No shadows, constant everywhere |

## Natural vs Artificial
- **Natural** (sunlight, skylight): spectrally varying, unstable
- **Artificial** (LEDs, bulbs): controllable → simplifies vision algorithms

## Significance
Controlled illumination is a practical tool to reduce the complexity of vision algorithms — it is why industrial vision systems use structured lighting rather than relying on ambient light.
