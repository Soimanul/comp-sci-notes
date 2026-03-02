**Tags:** #concept #computer-vision
**Related:** [[Affine Transformation]], [[Rotation Matrices]], [[Geometric Transformations]]

## Definition
A Euclidean transformation (rigid body transformation) is a geometric transformation that preserves distances and angles. It consists of a rotation and a translation only.

## Matrix Form (2D)
Using homogeneous coordinates, a 2D Euclidean transformation has **3 degrees of freedom** (1 rotation angle, 2 translation components):

$$
\begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} = \begin{pmatrix} \cos\theta & -\sin\theta & t_x \\ \sin\theta & \cos\theta & t_y \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}
$$

## Preserved Properties
- All distances
- All angles
- Shape and size

Euclidean transformations are a special case of [[Affine Transformation]].

## Estimation
Requires **2 point correspondences** to solve for the 3 degrees of freedom.

## Significance
Euclidean transformations model rigid motion — used in tracking, medical image registration, and robot odometry where shape and scale must be preserved.
