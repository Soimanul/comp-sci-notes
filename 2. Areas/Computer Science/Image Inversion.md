## Related
- [[Pinhole Camera Model]], [[Magnification]]

## Definition
Image inversion refers to the fact that images formed by a pinhole or ideal pinhole-like camera are **flipped upside down** relative to the scene.

## Core Ideas
- Rays of light cross at the pinhole; points above the optical axis map below it, and vice versa.
- This inversion is a geometric consequence of the projection model, not a physical artifact of lenses.

## Mathematical Formulation
In the pinhole projection equations:
$$
x = f \cdot \frac{X}{Z},\quad
y = f \cdot \frac{Y}{Z}
$$
the sign of the coordinates (with focal distance defined behind the pinhole) produces an **inverted** image when interpreted relative to scene orientation.

If $Z > 0$, and we define $f > 0$, this conventionally yields the inverted orientation in the image plane.
