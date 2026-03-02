**Tags:** #concept #computer-vision
**Related:** [[Intrinsic & Extrinsic Parameters]], [[Linear Camera Model]], [[Homogeneous Coordinates]]

## Definition
The camera calibration matrix $K$ (also called the intrinsic matrix) encodes the mapping from camera coordinates to pixel coordinates. It captures all sensor-dependent parameters of the camera.

## Structure

$$
K = \begin{pmatrix} f_x & 0 & c_x \\ 0 & f_y & c_y \\ 0 & 0 & 1 \end{pmatrix}
$$

Where:
- $f_x, f_y$ — focal lengths in pixels (combining physical focal length $f$ and pixel size)
- $c_x, c_y$ — principal point: pixel offset of the optical axis from the sensor origin

Since pixel size and focal length cannot be separated without additional information, they are grouped: $f_x = f / \text{pixsize}_x$.

## Degrees of Freedom
$K$ has **5 intrinsic parameters**: $f_x, f_y, c_x, c_y$, and optionally a skew term (usually zero for modern cameras).

## Significance
$K$ is what makes a camera "calibrated." Knowing $K$ allows converting pixel coordinates back to angular directions in the scene, which is required for 3D reconstruction and augmented reality.
