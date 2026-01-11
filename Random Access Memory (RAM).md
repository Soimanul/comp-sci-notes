
**Tags:** #concept #cs #hardware **Related:** [[Arrays]]

# Definition

**RAM** (Random Access Memory) is the hardware in a computing device where the operating system, application programs, and data in current use are kept so they can be quickly reached by the device's processor.

# Conceptual Structure

Memory can be visualized as a giant grid or "Bit Matrix" (e.g., 32x32 bits).

- **Address:** Each cell (usually a byte) has a unique unique identifier called a memory address (e.g., `0xFE0FAB09`).
    
- **Process Memory:** When a program runs, it is assigned a specific range of addresses.
    

# Relation to Data Structures

The physical layout of memory dictates the performance of data structures.

- **[[Arrays]]** mirror the physical layout of RAM (contiguous blocks), enabling $O(1)$ access.
    
- **[[Linked Lists]]** scatter data across random addresses, requiring pointers to connect them, which forces sequential access.