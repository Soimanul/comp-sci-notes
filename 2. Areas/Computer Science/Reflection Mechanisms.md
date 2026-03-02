**Tags:** #concept #computer-vision
**Related:** [[Illumination Types]], [[Photometric Image Formation]], [[Image Sensing]]

## Definition
Reflection mechanisms describe how light interacts with a surface and determines whether it appears matte or glossy. Most real surfaces exhibit a mixture of both types.

## Types

### Surface (Specular) Reflection
- Occurs at smooth, polished surfaces
- Light re-emits in a mirror-like direction
- Produces **glossy highlights**

### Body (Diffuse) Reflection
- Occurs in non-homogeneous materials
- Light is scattered in all directions
- Produces **matte appearance**
- Modelled by **Lambert's cosine law**: $I \propto \cos\theta$ where $\theta$ is the angle between the surface normal and the light direction

## Hybrid Reflection
Most real objects exhibit **both** mechanisms simultaneously. The relative contribution determines the material's appearance along the matte-to-glossy spectrum.

## Significance
Understanding reflection is essential for interpreting pixel intensity: the same surface can look very different under different lighting because its reflection changes.
