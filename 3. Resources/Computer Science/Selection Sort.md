
**Tags:** #algorithm #sorting **Related:** [[Basic Sorting]], [[Arrays]]

# Definition

An in-place comparison sorting algorithm that divides the input list into two parts: a sorted sublist of items which is built up from left to right, and a sublist of the remaining unsorted items.

# Algorithm Logic

1. Set the first element as the "minimum".
    
2. Iterate through the rest of the array to find the actual minimum value.
    
3. Swap the found minimum with the first element.
    
4. Move the boundary of the sorted partition one element to the right.
    
5. Repeat for the remaining unsorted elements.

Animation:
![[selection-sort-0-dc86a88ab889d19e8ffad6cba3eb6e2f 1.gif]]
# Complexity Analysis

- **Worst Case:** $O(n^2)$.
    
- **Average Case:** $O(n^2)$.
    
- **Best Case:** $O(n^2)$ (It must scan the array to confirm the minimum every time, regardless of order).
    
# Comparison

Unlike [[Insertion Sort]], Selection Sort is **not** adaptive; it takes the same amount of time regardless of the initial order of elements.