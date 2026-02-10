**Tags:** #model #neural-networks 
**Related:** [[McCulloch-Pitts Neuron]], [[Bias (Neural Networks)]], [[Activation Functions]]

## Definition
An algorithm for supervised learning of binary classifiers, developed by Frank Rosenblatt (1958). It improves on the McCulloch-Pitts neuron by introducing **learnable weights**.

## Mathematical Formula
$$y = f(\sum_{i=1}^{n} w_i x_i + b)$$

- $w_i$: Weights (importance of each input).
- $x_i$: Inputs.
- $b$: [[Bias (Neural Networks)]] (Shift).
- $f$: [[Activation Functions]] (Step function).

## Structure 

![[perceptron_labeled (2).png]]

## Performance on data

![[Pasted image 20260128120653.png]]

## Significance
It was the first model that could learn from data by adjusting its weights to minimize error, forming the building block of modern Deep Learning.

## Perspectives from Courses
### Statistical Learning & Prediction
- **Limitation**: Only works for linearly separable data; the algorithm does not terminate unless perfect separation is achieved.
- **Arbitrary Boundaries**: When separable, it returns any arbitrary hyperplane that fits; some (like those with larger margins) are better than others.
- **Evolution**: Transitions to [[Logistic Regression]] by replacing the hard step function with a [[Sigmoid Function]] to enable probabilistic outputs and smoother gradients.

