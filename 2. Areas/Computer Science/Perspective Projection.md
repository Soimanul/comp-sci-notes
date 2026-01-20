**Tags:** #math #geometry #computer-vision **Related:** [[Geometric Image Formation]], [[Magnification]], [[Straight Line Preservation (Perspective Projection)]]

## Definition
A projection method where 3D points are mapped to the image plane via rays passing through a single **Center of Projection** (the pinhole).

## Mathematical Formulation
Derived from similar triangles. For a point $(X, Y, Z)$ and focal length $f$:

$$x = f \cdot \frac{X}{Z}$$$$y = f \cdot \frac{Y}{Z}$$
## Key Properties
1. **Scaling:** Image size is inversely proportional to depth ($1/Z$).
    
2. **Line Preservation:** Straight lines in 3D remain straight in 2D.
    
3. **Parallel Convergence:** Parallel lines in 3D converge to a [[Vanishing Point]] in 2D (unless parallel to the image plane).