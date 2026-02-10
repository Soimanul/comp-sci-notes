**Tags:** #concept #math #optimization
**Related:** [[Gradient Descent]], [[Stochastic Gradient Descent (SGD)]]

## Definition
A point on the surface of a loss function where the gradients in all directions are zero, but which is not a local minimum or maximum.

## The Challenge
In high-dimensional spaces (like those in deep learning), saddle points are far more common than local minima. 
- At a saddle point, the surface may be flat in some dimensions and curved in others.
- Standard [[Gradient Descent]] can slow down significantly or get "stuck" at these points because the gradient is zero.

## Solutions
- **[[Stochastic Gradient Descent (SGD)]]**: The inherent noise in mini-batch updates can provide the "kick" needed to move past a flat saddle point.
- **[[Momentum Gradient Descent]]**: Building up velocity allows the optimizer to "roll" through flat regions.
