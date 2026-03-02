**Tags:** #concept #computer-vision
**Related:** [[Affine Transformation]], [[RANSAC]], [[Panorama Stitching]], [[Geometric Transformations]]

## Definition
A homography (projective transformation) is a mapping between two images of the same planar surface from different viewpoints, or between two images taken by a camera undergoing pure rotation. It is the most general linear image transformation in homogeneous coordinates.

## Matrix Form
**8 degrees of freedom** (the $3 \times 3$ matrix $H$ is defined up to scale, so 9 entries − 1 = 8):

$$
\lambda \begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} = \begin{pmatrix} h_{11} & h_{12} & h_{13} \\ h_{21} & h_{22} & h_{23} \\ h_{31} & h_{32} & 1 \end{pmatrix} \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}
$$

## What It Can Do
- Everything an affine transformation can
- Additionally: **parallel lines may converge** (perspective foreshortening)

## Key Applications
- **Perspective correction**: rectify a tilted planar surface (e.g., a document)
- **Panorama stitching**: align overlapping images taken with a fixed camera position

## Estimation
Requires **4 point correspondences**. In practice, many noisy correspondences are used with [[RANSAC]] to robustly estimate $H$.

## Significance
Homography is the fundamental tool for planar scene reconstruction and image alignment. It directly models the geometry of a camera change for flat scenes.
