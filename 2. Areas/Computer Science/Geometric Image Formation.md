**Tags:** #concept #computer-vision #geometry **Related:** [[Image Formation]], [[Pinhole Camera Model]], [[Perspective Projection]]

## Definition
Geometric image formation is the process of mapping a 3D point in the world $\mathbf{P}_o = (X, Y, Z)$ to a specific 2D location $\mathbf{P}_i = (x, y)$ on the image sensor.

## Core Mechanism: Similar Triangles
The geometry is governed by the **Pinhole Model**. By observing the similar triangles formed by the optical axis and the light ray:

$$\frac{x}{f} = \frac{X}{Z} \implies x = f \cdot \frac{X}{Z}$$

- $f$ **(Focal Length):** The distance from the center of projection (pinhole) to the image plane.
    
- $Z$ **(Depth):** The distance of the object from the camera.
    
- $X$ **(Object Size):** The physical height/width of the object.

## Key Geometric Properties
1. **Scaling:** Image size is inversely proportional to depth ($1/Z$). Objects twice as far appear half as big.
    
2. **[[Magnification]]:** Controlled by the ratio $f/Z$. To make an object larger, you either move closer (decrease $Z$) or zoom in (increase $f$).
    
3. **Line Preservation:** Straight lines in 3D project to straight lines in 2D (except when passing through the optical center).
    
## [[Field of View]] (FOV)

