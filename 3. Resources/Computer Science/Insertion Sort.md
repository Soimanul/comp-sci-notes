
**Tags:** #algorithm #sorting **Related:** [[Basic Sorting]], [[Arrays]]

# Definition

An in-place comparison sorting algorithm that builds the final sorted array one item at a time. It assumes the first element is already sorted, then takes the next element and places it in the correct position relative to the sorted portion.

# Algorithm Logic

1. Start from the second element (index 1).
    
2. Compare the current element (key) with the elements in the sorted sub-list (to its left).
    
3. Shift all elements in the sorted sub-list that are greater than the key to the right.
    
4. Insert the key into the correct position.
    
5. Repeat until the array is fully sorted.

Animation
![[insertion-sort-e8e40865ca8316a75a00ae32347acffb.gif]]

# Complexity Analysis

- **Worst Case:** $O(n^2)$ (Array is in reverse order).
    
- **Average Case:** $O(n^2)$.
    
- **Best Case:** $O(n)$ (Array is already sorted).

# Use Cases

- Small datasets.
    
- Data that is already "nearly" sorted (adaptive).