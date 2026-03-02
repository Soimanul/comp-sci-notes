**Tags:** #concept #computer-vision
**Related:** [[Homography]], [[Panorama Stitching]], [[Camera Calibration]], [[Geometric Transformations]]

## Definition
RANSAC (RANdom SAmple Consensus) is a robust model fitting algorithm designed for datasets with a high proportion of outliers. It iteratively hypothesises a model from a minimal sample and counts its support.

## Algorithm

```
Input: data points, model, error function, inlier threshold ε, iterations N
Best model ← None;  max inliers ← 0

Repeat N times:
  1. Randomly select minimum sample (e.g., 4 points for a homography)
  2. Fit model to sample
  3. Count inliers: points with error < ε
  4. If inlier count > max inliers:
       best model ← current model
       max inliers ← inlier count

Refit model using ALL inliers of best model
Output: estimated model, set of inliers
```

## Key Parameters
- $N$ (iterations) — more iterations → higher probability of finding the true model
- $\varepsilon$ (inlier threshold) — depends on expected noise level
- Minimum sample size — determined by the model (2 for line, 4 for homography)

## Why It Works
With enough iterations, there is a high probability that at least one sample will contain only inliers, yielding a good model estimate.

## Significance
RANSAC is the de facto standard for robust geometric estimation in computer vision — used in feature matching, panorama stitching, structure from motion, and visual odometry.
