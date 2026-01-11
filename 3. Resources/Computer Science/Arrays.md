
**Tags:** #data-structure #linear #cs **Related:** [[Random Access Memory (RAM)]], [[Linked Lists]], [[Sequential Search]], [[Multidimensional Arrays]]

# Definition

An array is a collection of items stored at **contiguous memory locations**. The idea is to store multiple items of the same type together.
![[array.png]]
# Memory Access Math

Arrays allow for **Random Access**, meaning you can access any element in constant time $O(1)$. This is possible because the computer can calculate the exact memory address of an element using a simple formula:

$$\text{Address} = \text{Base\_Address} + (\text{Index} \times \text{Size\_of\_Element})$$

Because the memory is contiguous and element sizes are fixed, the computer does not need to iterate through the data to find index 5; it jumps directly to the calculated address.
5 x
# Complexity Analysis

| Operation             | Complexity | Note                                                   |
| --------------------- | ---------- | ------------------------------------------------------ |
| **Read (Access)**     | $O(1)$     | Instant access via math.                               |
| **Write (Overwrite)** | $O(1)$     | If index is known.                                     |
| **Insert**            | $O(n)$     | Requires shifting subsequent elements to make space.   |
| **Delete**            | $O(n)$     | Requires shifting subsequent elements to fill the gap. |
|                       |            |                                                        |
# Constraints

- **Fixed Size:** In low-level languages (C, Java), arrays have a fixed size determined at creation.
    
- **Homogeneous:** Usually store elements of the same data type.