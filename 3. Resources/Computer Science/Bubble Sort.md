
**Tags:** #algorithm #sorting **Related:** [[Basic Sorting]], [[Arrays]]

# Definition

A simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

# Algorithm Logic

1. Iterate through the array from the beginning.
    
2. Compare element $i$ with element $i+1$.
    
3. If element $i > i+1$, swap them.
    
4. After one full pass, the largest element "bubbles up" to the last position.
    
5. Repeat the process for the remaining elements ($n-1$, $n-2$, etc.) until no swaps are needed.

Animation:
![[bubble-sort-0-dc86a88ab889d19e8ffad6cba3eb6e2f.gif]]    
# Complexity Analysis

- **Worst Case:** $O(n^2)$ (Reverse order).
    
- **Average Case:** $O(n^2)$.
    
- **Best Case:** $O(n)$ (If optimized with a "swapped" flag to detect if the array is already sorted).