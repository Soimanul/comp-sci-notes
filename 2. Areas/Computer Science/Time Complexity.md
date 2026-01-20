
**Tags:** #concept #cs **Related:** [[Algorithm Analysis]], [[Big O Notation]]

# Definition

Time complexity is a function $T(n)$ that describes the running time of an algorithm in terms of the size of the input ($n$). It does not measure time in seconds, but rather in the **number of operations** executed.

# Calculating T(n)

To find the time complexity, we sum the cost of each line of code multiplied by the number of times it is executed.

## Example Analysis

```python
def calculate(n):
    x = 0               # c1 (executed 1 time)
    for i in range(n):  # c2 (executed n times)
         x += i         # c3 (executed n times)
    return x            # c4 (executed 1 time)
```

**Exact Function:** $T(n) = c_1 + n(c_2 + c_3) + c_4$ **Asymptotic Analysis:** As $n$ grows large, the linear term $n$ dominates the constant terms. **Result:** $O(n)$.

# Input Size

The definition of "Input Size" ($n$) depends on the problem:

- **Sorting/Searching:** $n$ is the number of items in the list.
    
- **Graphs:** $n$ is often $|V|$ (vertices) and $|E|$ (edges).
    
- **Arithmetic:** $n$ is the number of bits needed to represent the number.