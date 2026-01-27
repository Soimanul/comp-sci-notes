**Tags:** #concept #neural-networks #history 
**Related:** [[Perceptron]]

## Definition
The earliest mathematical model of a biological neuron (1943). It functions as a binary linear classifier (a logic gate).

## Mechanism
1. **Inputs:** Binary signals ($x_1, x_2...$).
2. **Aggregation:** Sums the inputs ($g(x) = \sum x_i$).
3. **Threshold:** If the sum exceeds a fixed threshold $\theta$, the neuron fires (Output 1); otherwise, it stays silent (Output 0).
    
## Limitation
It has **no weights** and **no bias**. It cannot "learn"; the parameters must be manually set to create logic gates like AND/OR.