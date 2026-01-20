**Tags:** #model #neural-networks #deep-learning **Related:** [[Multilayer Perceptron]], [[Backpropagation]]

## Definition
A Feedforward Neural Network (FNN) is the simplest type of artificial neural network wherein connections between the nodes do **not** form a cycle.

## Mechanism

- **Unidirectional Flow:** Information moves in only one direction—forward—from the input nodes, through the hidden nodes (if any), and to the output nodes.
    
- **No Loops:** Unlike Recurrent Neural Networks (RNNs), there are no feedback loops; the output of a layer never affects the same layer.

## Architecture
It is essentially a directed acyclic graph.

1. **Input Layer:** Receives the feature vector.
    
2. **Hidden Layers:** Perform non-linear transformations (using [[Activation Functions]]).
    
3. **Output Layer:** Produces the final prediction.

![[Pasted image 20260116111433.png]]