**Tags:** #concept #computer-vision #signal-processing
**Related:** [[Convolution]], [[Point Spread Function]], [[Gaussian Filter]]

## Definition
A Linear Shift Invariant (LSI) system is a system whose output is a linear combination of its inputs (linearity) and whose behaviour does not change with spatial position (shift invariance). All LSI systems perform convolution.

## The Two Properties

**Linearity:**
$$\mathcal{H}\{af + bg\} = a\mathcal{H}\{f\} + b\mathcal{H}\{g\}$$

**Shift invariance:** shifting the input by $\Delta$ shifts the output by $\Delta$ — the system's response does not depend on where in the image something occurs.

## Key Result
Any LSI system is completely characterised by its **impulse response** (or **kernel**). The output for any input is the **convolution** of the input with the impulse response:

$$g = f * h$$

where $h$ is the system's response to a [[Point Spread Function|unit impulse]].

## Significance
The LSI framework provides a unified theory for all linear image filters. It explains why filtering can be described purely by a kernel, and justifies using the Fourier transform for efficient implementation via the [[Convolution Theorem]].
