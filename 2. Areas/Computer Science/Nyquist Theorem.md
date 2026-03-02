**Tags:** #concept #computer-vision #signal-processing
**Related:** [[Aliasing]], [[2D Fourier Transform]], [[Fourier Transform Applications]], [[Pixel Size & Resolution]]

## Definition
The Nyquist–Shannon sampling theorem states that a continuous signal can be perfectly reconstructed from its samples if and only if the sampling rate is **greater than twice** the highest frequency in the signal.

## Nyquist Rate

$$f_{\text{sample}} > 2 f_{\text{max}}$$

Or equivalently, the sampling interval $\Delta$ must satisfy:

$$\Delta < \frac{1}{2 f_{\text{max}}}$$

## What Happens When Violated
If the signal contains frequencies above $f_{\text{sample}}/2$ (the **Nyquist frequency**), those high frequencies are **aliased** — they appear as false lower frequencies in the sampled signal. See [[Aliasing]].

## In Images
- The "sampling rate" is the pixel density (pixels per mm)
- The "highest frequency" is the finest detail in the scene (set by the lens)
- The Nyquist frequency = half the pixel density
- Anti-aliasing filter (optical low-pass filter) removes frequencies above the Nyquist limit before the sensor

## Mathematical View
Sampling in the spatial domain = multiplying by an impulse train. In the Fourier domain, this causes the spectrum to repeat (replicate). Aliasing occurs when these replicated copies overlap.

## Significance
The Nyquist theorem defines the fundamental limit of digital imaging: there is no benefit in having more pixels than twice the optical resolution, and too few pixels cause aliasing artefacts.
