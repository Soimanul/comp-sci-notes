**Tags:** #concept #computer-vision
**Related:** [[Euclidean Transformation]], [[Homography]], [[Image Warping]], [[Geometric Transformations]]

## Definition
An affine transformation is a linear mapping followed by a translation that preserves parallelism. It generalises the Euclidean transformation by adding scaling and shearing.

## Matrix Form (2D)
**6 degrees of freedom**:

$$
\begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} = \begin{pmatrix} a_{11} & a_{12} & t_x \\ a_{21} & a_{22} & t_y \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}
$$

## Operations Captured
- Translation
- Rotation
- Reflection
- Uniform and non-uniform scaling
- Shearing

## Preserved Properties
- **Parallel lines remain parallel** (the defining property)
- Straight lines remain straight
- Ratios of lengths along a line

## Estimation
Requires **3 point correspondences** to solve for 6 degrees of freedom.

## Significance
Affine transformations model camera changes that don't change viewpoint significantly (e.g., small zoom changes, document scanning). They are a computationally cheaper alternative to homography when the scene is approximately planar.
