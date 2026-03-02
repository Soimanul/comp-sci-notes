**Tags:** #concept #computer-vision
**Related:** [[Camera Calibration Matrix]], [[Rotation Matrices]], [[Linear Camera Model]]

## Definition
Camera parameters are split into **intrinsic** (sensor-dependent) and **extrinsic** (pose-dependent) components, together forming the full camera projection matrix $P = K[R \mid t]$.

## Intrinsic Parameters (Camera Calibration Matrix $K$)
Describe the internal geometry of the camera:
- $f_x, f_y$ — focal lengths in pixels
- $c_x, c_y$ — principal point (image centre offset)
- (Optional) skew coefficient

These are **fixed** for a given camera and lens.

## Extrinsic Parameters ($[R \mid t]$)
Describe the camera's pose in the world:
- $R$ — $3 \times 3$ rotation matrix (3 degrees of freedom)
- $t$ — $3 \times 1$ translation vector (3 degrees of freedom)

These **change** when the camera is moved.

## Combined Model

$$
P = K \begin{bmatrix} R & t \end{bmatrix}
$$

This $3 \times 4$ projection matrix maps a 3D world point (homogeneous) directly to a 2D image point (homogeneous).

## Significance
Separating intrinsic and extrinsic parameters allows cameras to be re-used across scenes: calibrate once (intrinsics), then update only the pose (extrinsics) per scene.
