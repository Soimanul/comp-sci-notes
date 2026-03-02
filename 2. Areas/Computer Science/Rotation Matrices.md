**Tags:** #concept #computer-vision #linear-algebra
**Related:** [[Intrinsic & Extrinsic Parameters]], [[Linear Camera Model]], [[Homogeneous Coordinates]]

## Definition
Rotation matrices are orthogonal matrices used to represent rigid rotations in 2D or 3D space. In the camera model, they form the rotational part of the extrinsic matrix.

## Properties
- $R^T = R^{-1}$ (orthogonal)
- $\det(R) = 1$ (proper rotation, no reflection)
- Columns (and rows) are orthonormal vectors

## 2D Rotation

$$
R(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}
$$

## 3D Rotation
3D rotations are composed of rotations around each axis ($R_x, R_y, R_z$), e.g.:

$$
R_z(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{pmatrix}
$$

Alternative representations: **axis–angle** and **quaternions** (avoid gimbal lock and are more numerically stable).

## Significance
The 3 rotation parameters define how the camera is oriented in the world. Together with the 3 translation parameters, they form the extrinsic matrix $[R \mid t]$ that places the camera in the scene.
