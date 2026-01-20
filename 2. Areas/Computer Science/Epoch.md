**Tags:** #concept #neural-networks #training **Related:** [[Backpropagation]], [[Feedforward Neural Network]]

## Definition
In machine learning training, an **Epoch** is defined as one complete pass of the entire training dataset through the learning algorithm.

## Context
Training a neural network usually requires multiple epochs.

- **One Pass:** The network sees every example once, makes predictions, calculates errors, and updates weights via [[Backpropagation]].
    
- **Why Multiple?** Gradient Descent is an iterative process. Seeing the data once is rarely enough to converge to an optimal solution (minimum error).

## Relation to Batch
- **Batch:** A subset of the dataset processed before updating weights.
- **Iteration:** The number of batches needed to complete one epoch.
- _Formula:_ $\text{Iterations} = \frac{\text{Total Examples}}{\text{Batch Size}}$