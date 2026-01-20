**Tags:** #concept #computer-vision #optics **Related:** [[Lens Aberrations]], [[Photometric Image Formation]]

## Definition

A reduction of an image's brightness or saturation toward the periphery (edges) compared to the image center.

## Causes

1. **Mechanical:** Light blocked by lens hood or filters.
    
2. **Optical/Natural:** Light hitting the sensor at an oblique angle results in lower intensity compared to the perpendicular rays at the center.
    

## Correction

Can be corrected mathematically by fitting a polynomial function to a "blank" (uniform) image to model the falloff, then dividing the raw image by this model.