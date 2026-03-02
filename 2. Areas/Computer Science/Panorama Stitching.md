**Tags:** #concept #computer-vision
**Related:** [[Homography]], [[RANSAC]], [[Image Warping]], [[Geometric Transformations]]

## Definition
Panorama stitching assembles multiple overlapping images of a scene into a single wide-angle image by estimating the [[Homography]] between adjacent frames.

## Pipeline
1. **Detect features** in each image (e.g., SIFT, ORB)
2. **Match features** across overlapping image pairs
3. **Estimate homography** using matched correspondences + [[RANSAC]] to remove outliers
4. **Warp** one image into the coordinate frame of the other via [[Image Warping]]
5. **Blend** the overlapping regions (e.g., weighted average, feathering)

## Blending Challenge
If the two images differ in brightness at the seam, simple averaging creates a visible edge. More advanced methods (multi-band blending, Poisson blending) produce seamless results.

## Limitation
Homography stitching is exact only for **planar scenes** or **pure camera rotation**. For scenes with depth variation and camera translation, parallax causes ghosting at object boundaries.

## Significance
Panorama stitching is one of the clearest demonstrations of homography applied to real images and is the basis for 360° photography and virtual tour creation.
