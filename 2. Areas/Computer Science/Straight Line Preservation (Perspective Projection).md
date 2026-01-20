## Related
- [[Perspective Projection]], [[Geometric Image Formation]]

## Definition
Under perspective projection, any straight line in 3D space projects to a straight line in the 2D image.

## Core Ideas
- This property follows from the projective geometry of perspective cameras.
- If 3D points lie on a line, their projections also lie on a line.
- This makes line detection and reconstruction predictable in computer vision.

## Mathematical Formulation
If 3D points on a line are parametrized as:
$$
(X(t), Y(t), Z(t)) = (X_0 + t \cdot d_X,\; Y_0 + t \cdot d_Y,\; Z_0 + t \cdot d_Z)
$$
then after projection:
$$
x(t) = f \cdot \frac{X(t)}{Z(t)},\quad
y(t) = f \cdot \frac{Y(t)}{Z(t)}
$$
the parametric form remains linear in image coordinates.
