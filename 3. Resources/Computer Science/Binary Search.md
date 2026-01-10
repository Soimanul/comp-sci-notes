
**Tags:** #concept #algorithm #search **Related:** [[Divide and Conquer Strategy]], [[Arrays]], [[Logarithms]]

# Definition

Binary Search is an efficient algorithm to find a target value within a **sorted array**. It works by repeatedly dividing the search interval in half.
# Explanation

Binary Search uses the **Divide and Conquer** strategy:

1. Compare the target value to the middle element of the array.

2. If they are equal, the position is found.

3. If the target is smaller, search the left half.

4. If the target is larger, search the right half.

5. Repeat until the target is found or the subarray is empty.


**Constraint:** The input array **must be sorted** (monotonically increasing or decreasing).
# Complexity Analysis

- **Time Complexity:** $O(\log n)$
	- In the worst case, the array size is halved in every step. For an array of size $N$, the max number of steps is $\log_2 N$.
- **Space Complexity:**
	- Iterative: $O(1)$
	- Recursive: $O(\log n)$ (due to call stack overhead).

# Implementations

_Click to view specific language syntax._

- [[Binary Search - Python]]