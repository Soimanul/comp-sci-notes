
**Tags:** #concept #math **Related:** [[Algorithm Analysis]], [[Binary Search]]

# Definition

Logarithms are the inverse operation of exponentiation. In Computer Science, we almost always deal with **binary logarithms** (base 2).

Formula: $y = \log_b(x)$ is equivalent to $b^y = x$.

# Why it matters in CS

Logarithms appear whenever an algorithm uses a "Divide and Conquer" strategy, specifically when the problem size is halved in each step.

## Derivation for Halving

If we start with $N$ items and divide by 2 repeatedly, how many steps ($x$) until we reach 1 item?

$$1 = N / 2^x$$$$2^x = N$$$$x = \log_2 N$$

This is why algorithms like [[Binary Search]] and [[Merge Sort]] have logarithmic components in their time complexity.

# Key Properties

- $\log(ab) = \log a + \log b$
    
- $\log(n^k) = k \log n$ (This is why $O(\log n^2)$ simplifies to $O(\log n)$)