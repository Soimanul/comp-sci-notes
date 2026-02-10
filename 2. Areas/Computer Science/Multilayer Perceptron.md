**Tags:** #concept #model #neural-networks #deep-learning 
**Related:** [[Perceptron]], [[Feedforward Neural Network]], [[SLP - Multi-Layer Perceptrons]], [[Backpropagation]]

## Definition
A Multi-Layer Perceptron (MLP) is a class of feedforward artificial neural network consisting of an input layer, one or more hidden layers, and an output layer. It is the fundamental building block of modern deep learning.

## Mechanism
Unlike a single [[Perceptron]], which can only classify linearly separable data (e.g., AND/OR gates), an MLP can solve non-linear problems (like the **XOR problem**). 

### Layer Roles
1. **Input Layer**: Receives feature vectors.
2. **Hidden Layers**: Perform non-linear [[Feature Transformation]]. 
3. **Output Layer**: Computes the final score or probability distribution (e.g., using [[Softmax Function]]).

## Geometric Interpretation
### Composition of Polygons
Each neuron in the hidden layer defines a linear decision boundary (a line in 2D, a plane in 3D). By combining these neurons, the hidden layer effectively creates a **convex polygon** (or polytope) in the feature space. The output neuron then performs an OR-like operation to determine if a point falls within the complex region defined by these combined boundaries.

### Space Transformation
A linear layer (matrix multiplication) can only rotate, reflect, scale, or shear the input space. Adding a non-linear [[Activation Functions]] allows the network to **warp** or **fold** the space, bringing points that were originally far apart (and non-linearly separable) closer together so they can be separated by a single plane.

## Visualizations
![[SCR-20260128-kwns.png]]
![[Pasted image 20260128120338.png]]
![[Pasted image 20260128120945.png]]

## Significance
The inclusion of hidden layers and non-linear [[Activation Functions]] allows MLPs to act as universal function approximators.