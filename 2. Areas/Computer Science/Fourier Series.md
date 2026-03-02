**Tags:** #concept #computer-vision #signal-processing
**Related:** [[Fourier Transform (Concept)]], [[Discrete Fourier Transform]], [[Fourier Transform]]

## Definition
A Fourier series is the representation of a periodic function as an infinite weighted sum of sinusoids (sines and cosines) at integer multiples of a fundamental frequency.

## Core Idea

Any periodic function $f(t)$ with period $T$ can be written as:

$$f(t) = \sum_{k=-\infty}^{\infty} c_k \, e^{i 2\pi k t / T}$$

where the **Fourier coefficients** $c_k$ are:

$$c_k = \frac{1}{T} \int_0^T f(t) \, e^{-i 2\pi k t / T} \, dt$$

Each coefficient $c_k$ measures how much of frequency $k/T$ is present in the signal.

## Interpretation
- $k = 0$: DC component (mean value of $f$)
- $k = 1$: fundamental frequency (one full cycle per period)
- Higher $|k|$: higher harmonics (faster oscillations)
- Adding more terms → better approximation of the original function

## Significance
Fourier series show that any periodic signal is a mixture of pure sinusoids. This motivates the Fourier transform: the same decomposition principle applied to non-periodic signals.
