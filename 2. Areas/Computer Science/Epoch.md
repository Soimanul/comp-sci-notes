**Tags:** #concept #neural-networks #training 
**Related:** [[Backpropagation]], [[Feedforward Neural Network]]

## Definition
In machine learning training, an **Epoch** is defined as one complete pass of the entire training dataset through the learning algorithm. Thus, it encapsulates the $forward \ \ pass + backpropagation \ \ of \ \ the \ \ errors$.
## Context
Training a neural network usually requires multiple epochs.

- **One Pass:** The network sees every example once, makes predictions, calculates errors, and updates weights via [[Backpropagation]].
    
- **Why Multiple?** Gradient Descent is an iterative process. Seeing the data once is rarely enough to converge to an optimal solution (minimum error).


The backpropagation can be done in different ways depending on some choices we make:

• Do we use all the data (Batch)?

• Just one point (Stocastic Gradient Descent)?

• Some of them maybe (Mini Batch)?
## Relation to Batch
- **Batch:** A subset of the dataset processed before updating weights.
- **Iteration:** The number of batches needed to complete one epoch.
- _Formula:_ $\text{Iterations} = \frac{\text{Total Examples}}{\text{Batch Size}}$

