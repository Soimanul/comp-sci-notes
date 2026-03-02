**Tags:** #concept #computer-vision
**Related:** [[Dynamic Range]], [[Image Sensors]], [[Image Sensing]]

## Definition
High Dynamic Range (HDR) imaging captures a wider range of brightnesses than a single standard exposure allows, by combining multiple images taken at different exposure settings.

## Exposure Bracketing
The standard HDR approach:
1. Take $k$ images of the same static scene with exposures $e_0 < e_1 < \ldots < e_{k-1}$
2. Short exposures are well-exposed for bright regions; long exposures for dark regions
3. Combine all images using the known **camera response function** (CRF) to produce a single linear radiance map

## Ghost Artefacts
When there is motion between exposures, moving objects appear in different positions across bracketed images — producing **ghosting**. This is a fundamental limitation of multi-shot HDR.

## Single-Shot HDR
Alternative: assign different exposures **per pixel** (e.g., by overlaying a spatially varying neutral density filter). Missing information is recovered via interpolation.

## Significance
HDR imaging is critical in scenes with both bright sunlight and deep shadows (e.g., outdoor robotics, surveillance). It is standard in modern smartphones via computational photography.
