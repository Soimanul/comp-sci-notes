**Tags:** #concept #neural-networks
**Related:** [[Single Neuron Computation]], [[Feedforward Neural Network]], [[Activation Functions]]

## Definition
A neural network layer applies the same neuron computation to many neurons in parallel by replacing the weight vector with a matrix:
$$h = \sigma\!\left(W x + b\right)$$
where $x \in \mathbb{R}^n$, $W \in \mathbb{R}^{m \times n}$, $b \in \mathbb{R}^m$, and $\sigma$ is applied componentwise. The output $h \in \mathbb{R}^m$ is a new vector representation.

> [!info] Key Intuition
> A layer is not "many neurons" conceptually — it is one matrix multiplication followed by a componentwise nonlinearity. The matrix $W$ packs all weight vectors as rows; $Wx + b$ scores all neurons at once.

## Mechanics
- Each row $W_i$ of $W$ corresponds to the weight vector of neuron $i$; its output coordinate is $h_i = \sigma(W_i x + b_i)$.
- $Wx + b$ is a linear (affine) map from $\mathbb{R}^n$ to $\mathbb{R}^m$.
- $\sigma$ then bends that linear map into a nonlinear feature space.

> [!example]- Worked Example
> Two-neuron layer with $W = \begin{pmatrix} 1 & 0 \\ -1 & 2 \end{pmatrix}$, $b = (0, 1)$, $x = (3, 2)$, ReLU activation:
> - $Wx + b = (3, 2)$
> - $h = (\max(0,3), \max(0,2)) = (3, 2)$

## Significance
This compact form is the entire forward pass of a fully-connected layer. Composing several such transformations yields a feedforward neural network capable of representing complex nonlinear functions.
