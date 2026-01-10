
**Tags:** #topic #cs #algorithm-analysis **Related:** [[Big O Notation]], [[Time Complexity]], [[Logarithms]]

# Definition

Algorithm analysis is the process of determining the computational complexity of an algorithm, which is comprise of the amount of time, storage, or other resources needed to execute it.

The goal is to predict the performance of an algorithm as the input size ($n$) grows, without needing to implement it on a specific machine.

# Key Concepts

- **[[Time Complexity]]:** Describes the running time as a function of the input size $T(n)$.
    
- **[[Big O Notation]]:** The standard notation used to classify algorithms by their worst-case growth rates.
    
- **[[Logarithms]]:** Essential for analyzing divide-and-conquer algorithms (like Binary Search).
    

# Asymptotic Equivalence

We look for the asymptotic equivalence ($f(n) \sim g(n)$) where the limit of the ratio between the actual time and the approximated function approaches 1 as $n \to \infty$. This allows us to ignore constants and lower-order terms.
