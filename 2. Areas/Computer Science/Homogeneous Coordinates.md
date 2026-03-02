**Tags:** #concept #computer-vision #linear-algebra
**Related:** [[Linear Camera Model]], [[Camera Calibration Matrix]], [[Perspective Projection]]

## Definition
Homogeneous coordinates represent $n$-dimensional points in $(n+1)$-dimensional space, enabling perspective projection and translation to be expressed as matrix multiplications.

## Core Mechanics

A 2D point $(x, y)$ is represented in homogeneous coordinates as $(x, y, 1)$ — or equivalently any scalar multiple $(\lambda x, \lambda y, \lambda)$. To recover Cartesian coordinates, divide by the last component:

$$
(\tilde{x}, \tilde{y}, \tilde{w}) \rightarrow \left(\frac{\tilde{x}}{\tilde{w}},\ \frac{\tilde{y}}{\tilde{w}}\right)
$$

The same idea extends to 3D points: $(X, Y, Z) \rightarrow (X, Y, Z, 1)$.

## Why It Matters for Projection

The perspective projection equations are non-linear in Cartesian coordinates:

$$
x = f \cdot \frac{X}{Z}, \quad y = f \cdot \frac{Y}{Z}
$$

In homogeneous coordinates, this division by $Z$ becomes a linear operation, allowing the full camera model to be written as a single matrix multiplication:

$$
\lambda \begin{pmatrix} u \\ v \\ 1 \end{pmatrix} = K [R \mid t] \begin{pmatrix} X \\ Y \\ Z \\ 1 \end{pmatrix}
$$

## Significance
Without homogeneous coordinates, the camera projection model cannot be expressed as a linear system — making optimization and calibration far harder. They are the mathematical glue of projective geometry.
