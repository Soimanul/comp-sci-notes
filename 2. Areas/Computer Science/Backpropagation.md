**Tags:** #concept #algorithm #training
**Related:** [[Gradient Descent]], [[Multilayer Perceptron]], [[SLP - Backpropagation & Regression]]

## Definition
The algorithm used to train neural networks. It efficiently calculates the gradient of the loss function with respect to each weight in the network by applying the chain rule.

## Mechanism
1. **Forward Pass:** Compute the output and the error (Loss). The network is viewed as a **Computational Graph** of local operations.
   
2. **Backward Pass:** Propagate the error backward using the **Chain Rule**. Each node in the graph computes its local gradient and multiplies it by the incoming gradient from the right (upstream).
   
3. **Update:** Adjust weights using [[Gradient Descent]].

## Notation & Shortcuts
To understand the derivatives, we use the following standard notation:
- $L$: **Total Loss** (the error we aim to minimize).
- $a$: **Activation** (the output of a neuron, e.g., $a = \sigma(z)$).
- $z$: **Weighted Sum / Score** (the linear part of the neuron, $z = wx + b$).
- $x$: **Input** (the activation from the previous layer).

### Derivative Shortcuts
Due to the linear nature of $z = wx + b$, two derivatives always resolve to simple values:

- **Weight Gradient**: $\frac{\partial z}{\partial w} = x$ (The local gradient of the score($z$) w.r.t. the weight is simply the input value).

- **Bias Gradient**: $\frac{\partial z}{\partial b} = 1$ (The local gradient of the score($z$) w.r.t. the bias is always 1).

## How to Compute: General Gradient Rules
By applying the chain rule, we decompose the total gradient into three local components:

**For Weights ($w$):**
$$\frac{\partial L}{\partial w} = \frac{\partial L}{\partial a} \cdot \frac{\partial a}{\partial z} \cdot \frac{\partial z}{\partial w} \implies \frac{\partial L}{\partial a} \cdot \frac{\partial a}{\partial z} \cdot x$$

**For Biases ($b$):**
$$\frac{\partial L}{\partial b} = \frac{\partial L}{\partial a} \cdot \frac{\partial a}{\partial z} \cdot \frac{\partial z}{\partial b} \implies \frac{\partial L}{\partial a} \cdot \frac{\partial a}{\partial z} \cdot 1$$

### Derivative Cheat Sheet
| Component         | Function $f(z)$            | Derivative $f'(z)$                                                                                                              |
| :---------------- | :------------------------- | :------------------------------------------------------------------------------------------------------------------------------ |
| **Sigmoid**       | $\frac{1}{1+e^{-z}}$       | $\sigma(z)(1-\sigma(z))$                                                                                                        |
| **ReLU**          | $\max(0, z)$               | $1$ if $z > 0$, else $0$                                                                                                        |
| **MSE Loss**      | $\frac{1}{2}(y-\hat{y})^2$ | $(\hat{y} - y)$                                                                                                                 |
| **Cross-Entropy** | $-\sum y \log(\hat{y})$    | $(\hat{y} - y)$ (at the score level $z$) assuming one hot vector of true class was subtracted from the activation/output vector |

## Significance
Backpropagation allowed for the training of deep networks by solving the problem of how to assign "*blame*" for an error to hidden layers that do not have a direct target label.