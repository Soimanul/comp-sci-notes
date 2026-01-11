
**Tags:** #concept #cs **Related:** [[Algorithm Analysis]], [[Time Complexity]]
# Definition

Big O notation ($O$) describes the **upper bound** of an algorithm's running time. It represents the worst-case scenario: the 
algorithm will never perform worse than this limit.

While there are other notations, Big O is the industry standard for discussing efficiency.

- **Big O (**$O$**):** Worst case (Upper Bound).
    
- **Omega (**$\Omega$**):** Best case (Lower Bound).
    
- **Theta (**$\Theta$**):** Average case (Tight Bound).
    

# Common Orders of Growth

Listed from fastest to slowest.

| Notation      | Name         | Example                             |
| ------------- | ------------ | ----------------------------------- |
| $O(1)$        | Constant     | Accessing an array index            |
| $O(\log n)$   | Logarithmic  | [[Binary Search]]                   |
| $O(n)$        | Linear       | Simple Loop / [[Sequential Search]] |
| $O(n \log n)$ | Linearithmic | [[Merge Sort]], [[Quicksort]]       |
| $O(n^2)$      | Quadratic    | Nested Loops / [[Bubble Sort]]      |
| $O(2^n)$      | Exponential  | Recursive Fibonacci                 |
| $O(n!)$       | Factorial    | Traveling Salesman (Brute Force)    |
![[SCR-20260110-bxmg.png]]
# Calculation Rules

1. **Drop Constants:** $O(2n)$ becomes $O(n)$.
    
2. **Drop Non-Dominant Terms:** $O(n^2 + n)$ becomes $O(n^2)$.
    
3. **Logarithms Bases:** The base of the logarithm is usually ignored in Big O (assumed to be 2 in CS), so $O(\log_2 n)$ is written as $O(\log n)$.