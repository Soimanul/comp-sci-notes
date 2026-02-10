**Tags:** #concept #algorithm #optimization
**Related:** [[Gradient Descent]], [[SLP - Training Schedules & Hyperparameters]]

## Definition
An extension to [[Gradient Descent]] that helps accelerate gradients in the right direction and dampens oscillations.

## Mechanism
It adds a fraction $\gamma$ of the previous update vector to the current update:
$$v_t = \gamma v_{t-1} + \eta 
abla_	heta \mathcal{L}$$
$$	heta = 	heta - v_t$$

## Significance
Acts like a ball rolling down a hill; it builds "velocity" in directions of persistent decrease in loss, helping it move through flat regions or small local optima.
