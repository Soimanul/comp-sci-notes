**Tags:** #concept #computer-vision
**Related:** [[Camera Calibration Matrix]], [[Homogeneous Coordinates]], [[Intrinsic & Extrinsic Parameters]], [[Linear Camera Model & Calibration]]

## Definition
The linear camera model describes image formation as a linear mapping from 3D world coordinates to 2D image pixels using matrix multiplication — made possible by homogeneous coordinates.

## The Forward Model

Image formation has two steps:

1. **Change of basis** — transform world coordinates into camera coordinates using the extrinsic matrix $[R \mid t]$.
2. **Perspective projection** — project camera coordinates onto the image plane.

The full forward model in homogeneous coordinates:

$$
\lambda \begin{pmatrix} u \\ v \\ 1 \end{pmatrix} = K [R \mid t] \begin{pmatrix} X \\ Y \\ Z \\ 1 \end{pmatrix}
$$

Where:
- $K$ = camera calibration matrix (intrinsics)
- $[R \mid t]$ = rotation + translation (extrinsics)
- $\lambda$ = depth scale factor (homogeneous scaling)

## Degrees of Freedom
The model has **11 degrees of freedom** (5 intrinsic + 3 rotation + 3 translation), with one redundant scale factor, yielding effectively 10 independent parameters.

## Significance
The linear camera model is the foundation of 3D computer vision — it enables camera calibration, stereo reconstruction, and augmented reality by providing a mathematically tractable projection model.
