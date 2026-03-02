**Tags:** #concept #computer-vision
**Related:** [[Camera Calibration Matrix]], [[Intrinsic & Extrinsic Parameters]], [[Linear Camera Model]], [[Calibrated Stereo Vision]]

## Definition
Camera calibration is the process of estimating the intrinsic (and optionally extrinsic) parameters of a camera from images of a known geometric target (e.g., a checkerboard).

## Why Calibrate?
Measuring physical parameters (focal length, sensor size) directly is imprecise. Calibration instead solves for all parameters simultaneously using observed correspondences between:
- 3D world points $\mathbf{X}_i$ (known geometry of the target)
- 2D image points $\mathbf{x}_i$ (measured in the image)

## Method: Direct Linear Transform (DLT)
Each correspondence gives two linear equations in the 12 entries of $P = K[R \mid t]$. With $\geq 6$ correspondences, the system is overdetermined and solved via least-squares (SVD).

$$
\mathbf{x}_i \sim P \mathbf{X}_i
$$

Expanding gives:

$$
\begin{pmatrix} \mathbf{X}_i^T & 0 & -u_i \mathbf{X}_i^T \\ 0 & \mathbf{X}_i^T & -v_i \mathbf{X}_i^T \end{pmatrix} \mathbf{p} = 0
$$

where $\mathbf{p}$ is the vectorized form of $P$.

## Practical Notes
- Calibration also corrects for **lens distortion** (radial, tangential)
- More correspondences → better estimate
- Zhang's method (checkerboard) is the standard practical approach

## Significance
A calibrated camera converts pixel measurements into metric 3D quantities, enabling depth estimation, stereo vision, and augmented reality.
