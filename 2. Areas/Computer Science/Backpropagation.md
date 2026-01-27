**Tags:** #algorithm #neural-networks #training 
**Related:** [[Multilayer Perceptron]], [[Epoch]]

## Definition

The algorithm used to train neural networks. It efficiently calculates the gradient of the loss function with respect to each weight in the network.

## Mechanism

1. **Forward Pass:** Compute the output and the error (Loss).
    
2. **Backward Pass:** Propagate the error backward from the output layer to the input layer.
    
3. **Update:** Use the **Chain Rule** of calculus to determine how much each weight contributed to the error and adjust it (Gradient Descent).