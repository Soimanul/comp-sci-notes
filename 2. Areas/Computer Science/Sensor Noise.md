**Tags:** #concept #computer-vision
**Related:** [[Image Sensors]], [[Dynamic Range]], [[Image Sensing]]

## Definition
Sensor noise is any signal recorded by the sensor that does not correspond to genuine scene information. It is introduced at every stage of the imaging pipeline.

## Sources of Noise

### Scene-Dependent
| Type | Cause | Distribution |
|------|-------|--------------|
| **Photon shot noise** | Discrete, random photon arrivals | Poisson |

### Scene-Independent
| Type | Cause | Distribution |
|------|-------|--------------|
| **Read noise** | Imperfect charge-to-voltage conversion | Gaussian |
| **Quantization noise** | Digitization of continuous current | Uniform |
| **Dark current** | Thermal electron ejection | Poisson (temperature-dependent) |
| **Fixed pattern noise** | Defective pixels, pixel non-uniformity | Spatial pattern |

## Shot Noise Detail
Under identical illumination, the number of detected photons $N$ follows a Poisson distribution:
$$\text{Var}(N) = \mathbb{E}(N)$$

This means brighter regions have absolutely more noise but a better signal-to-noise ratio (SNR ∝ $\sqrt{N}$).

## Significance
Understanding noise sources guides denoising algorithm design — e.g., median filters address salt-and-pepper noise, Gaussian filters address read noise, and long-exposure averaging reduces shot noise.
