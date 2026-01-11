
**Tags:** #algorithm #search **Related:** [[Arrays]], [[Big O Notation]]

# Definition

Sequential Search (or Linear Search) is the simplest search algorithm. It checks every element in a list sequentially, starting from the first, until the desired element is found or the list ends.

# Algorithm Logic

1. Iterate from the first element (index 0) to the last.
    
2. Compare the current element with the target.
    
3. If they match, return `True` (or the index).
    
4. If the loop finishes without a match, return `False`.
    

# Complexity Analysis

- **Best Case:** $O(1)$ (Target is the first element).
    
- **Worst Case:** $O(n)$ (Target is the last element or not present).
    
- **Average Case:** $O(n/2) \approx O(n)$.
    

# Implementation (Python)

```python
def sequential_search(target, collection):
    for i in range(len(collection)):
        if collection[i] == target:
            return True
    return False
```

# When to use

- When the data is **unsorted**.
    
- When the dataset is small.
    
- When using data structures that do not support random access (like [[Linked Lists]]).