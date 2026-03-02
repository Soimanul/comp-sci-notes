**Tags:** #concept #computer-vision
**Related:** [[Pixel Size & Resolution]], [[Sensor Noise]], [[Dynamic Range]], [[Image Sensing]]

## Definition
An image sensor is a 2D array of photodetectors that converts incoming photons into electrical signals, which are then digitized into pixel values. Modern sensors are semiconductor-based.

## How It Works
When a silicon atom is hit by a visible photon, there is a probability that an electron moves to the **conduction band** (photoelectric effect). These electrons are collected at each **photodiode** pixel, and the accumulated charge is proportional to the number of detected photons.

## CCD vs CMOS

| | **CCD** (Charge-Coupled Device) | **CMOS** (Complementary Metal Oxide Semiconductor) |
|---|---|---|
| Readout | Charge shifted row by row to one amplifier | Each pixel read individually |
| Speed | Slower | Faster |
| Noise | Lower read noise | Higher read noise (improving) |
| Power | Higher | Lower |
| Use | Scientific/high-quality | Consumer cameras, phones |

## Key Properties
- [[Pixel Size & Resolution]]
- [[Sensor Noise]]
- [[Dynamic Range]]
- Quantum efficiency (QE) — fraction of photons that produce a detectable electron
- Frame rate / readout speed

## Significance
Sensor choice and properties determine the fundamental limits of image quality: resolution, noise, and the ability to capture fast or high-contrast scenes.
