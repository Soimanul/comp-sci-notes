**Tags:** #concept #computer-vision
**Related:** [[Camera Calibration]], [[Linear Camera Model]], [[Intrinsic & Extrinsic Parameters]]

## Definition
Calibrated stereo vision reconstructs the 3D coordinates of a scene point from its projections in two calibrated cameras by intersecting the two back-projected rays.

## The Core Problem
A single calibrated camera cannot determine the depth $Z$ of a scene point — the back-projected ray has infinite candidate 3D points. Two cameras provide two rays whose intersection gives a unique solution.

## Reconstruction Formula
Given:
- Image coordinates of a point in camera 1: $(u_1, v_1)$
- Image coordinates of the same point in camera 2: $(u_2, v_2)$
- Known camera matrices $P_1$, $P_2$
- Baseline $B$ (distance between cameras)

The world coordinates $(X, Y, Z)$ are found by solving the linear system formed by the projection equations of both cameras.

$$
Z \propto \frac{f \cdot B}{u_1 - u_2}
$$

where $u_1 - u_2$ is the **disparity**. Larger disparity = closer point.

## The Correspondence Problem
Stereo reconstruction requires finding which pixel in image 2 corresponds to a pixel in image 1. This is studied separately (feature matching, epipolar geometry).

## Output
A **depth map**: a per-pixel estimate of distance from the camera.

## Significance
Stereo vision is the simplest form of 3D reconstruction from images. It is used in autonomous driving, robotics, and medical imaging.
