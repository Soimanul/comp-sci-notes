**Tags:** #snippet #python

**Parent:** [[Binary Search]] 

---
## Implementation 

```python
def binary_search(arr, target):
	low = 0
	high = len(arr) - 1

	while low <= high:
		mid = (low + high) // 2
		guess = arr[mid]

		if guess == target:
			return mid
		if guess > target:
			high = mid - 1
		else:
			low = mid + 1

	return -1 # Target not found
```
## Syntax Notes

* **Integer Division:** Python uses `//` for floor division.

* **Overflow:** Python handles arbitrarily large integers automatically, so `(low + high) // 2` is safe from overflow errors common in Java/C++.