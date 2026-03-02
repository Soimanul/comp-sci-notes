**Tags:** #concept #computer-vision
**Related:** [[Colour Sensing]], [[Image Interpolation]], [[Image Sensors]]

## Definition
Demosaicing is the process of reconstructing a full-colour image from the raw output of a colour filter array (CFA) sensor, where each pixel records only one colour channel.

## The Problem
Camera sensors typically use a **Bayer filter mosaic**: a pattern of R, G, B filters over individual pixels (the most common pattern has twice as many green pixels as red or blue, matching human green sensitivity). Each pixel only captures one colour — the other two must be inferred.

## Bayer Pattern (Most Common CFA)
```
G R G R G R
B G B G B G
G R G R G R
B G B G B G
```

## Solution: Interpolation
Missing colour values are estimated from neighbouring pixels of the same colour channel. The simplest approach is **bilinear interpolation**: average the nearest same-colour neighbours.

More sophisticated methods use edge-aware interpolation to avoid colour fringing at sharp boundaries.

## Significance
Demosaicing is the first image processing step in virtually every digital camera. The quality of demosaicing affects sharpness, colour accuracy, and the appearance of artefacts (aliasing, moiré, colour fringing).
