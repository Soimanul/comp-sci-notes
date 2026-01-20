## Related
- [[Pinhole Camera Model]], [[Geometric Blur vs Diffraction Blur]], [[Exposure]]

## Definition
Pinhole size determines the trade-off between **geometric blur** (due to finite aperture size) and **diffraction blur** (due to wave optics). There exists an optimal pinhole diameter that minimizes total blur.

## Core Ideas
- A **large pinhole** admits many rays per scene point → geometric blur.
- A **very small pinhole** causes diffraction effects to dominate → wave spreading blur.
- Optimal design balances these to minimize overall blur.

## Mathematical Formulation (Conceptual)
The optimal pinhole diameter $d$ that balances geometric blur and diffraction is approximately:
$$
d \approx 2\sqrt{f\lambda}
$$
where:
- $f$ is the effective focal length,
- $\lambda$ is the wavelength of light.

This arises by equating geometric blur diameter with diffraction blur diameter in simplified models.
