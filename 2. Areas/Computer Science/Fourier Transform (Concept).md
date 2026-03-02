**Tags:** #concept #computer-vision #signal-processing
**Related:** [[Fourier Series]], [[Discrete Fourier Transform]], [[2D Fourier Transform]], [[Fourier Transform]]

## Definition
The Fourier transform decomposes a non-periodic continuous signal into a continuous spectrum of frequencies. It is a change of basis: the basis functions are complex exponentials (sinusoids of all frequencies).

## Forward Transform

$$F(\xi) = \int_{-\infty}^{\infty} f(t) \, e^{-i 2\pi \xi t} \, dt$$

$F(\xi)$ is a **complex number** for each frequency $\xi$:
- $|F(\xi)|$ — **magnitude spectrum**: how much energy at frequency $\xi$
- $\angle F(\xi)$ — **phase spectrum**: the phase offset of frequency $\xi$

## Inverse Transform

$$f(t) = \int_{-\infty}^{\infty} F(\xi) \, e^{+i 2\pi \xi t} \, d\xi$$

The inverse transform reconstructs the original signal from its spectrum. (Note the positive sign in the exponent.)

## Key Properties

| Property | Statement |
|----------|-----------|
| Linearity | $\mathcal{F}\{af + bg\} = a\hat{f} + b\hat{g}$ |
| Shift | Shift in time → phase shift in frequency |
| Convolution | $\mathcal{F}\{f * g\} = \hat{f} \cdot \hat{g}$ |

## Significance
The Fourier transform reveals the frequency content of any signal. In images, it separates slow-varying regions (low frequencies) from edges and fine details (high frequencies), enabling [[Frequency Domain Filtering]].
