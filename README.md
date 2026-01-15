# Dynamic-Set-Implementations

A Python implementation comparing two different data structures for representing dynamic sets: **Linked Lists** and **Arrays**. This project analyses the performance characteristics of both approaches through empirical testing.

## Overview

This project implements and compares two fundamental data structures used for dynamic sets:

- **Doubly Linked List**: Dynamic memory allocation with O(1) insertion/deletion
- **Array**: Contiguous memory with sequential storage

The comparison focuses on the `is_element()` operation, testing how each implementation performs when searching for elements in sets of 20,000 integers.

## Features

- **Doubly Linked List Implementation** - Full node-based dynamic set
- **Array-Based Implementation** - Sequential storage with shifting
- **Performance Testing** - Automated timing for 100 random lookups
- **Visualisation** - Scatter plot comparison of results
- **Detailed Reporting** - Results output to text file

## Project Structure

```
Dynamic-Set-Implementations/
├── src/
│   ├── DynamicSet.py       # Main implementation with both data structures
│   ├── plotter.py          # Visualisation utilities
│   └── tester.py           # Testing framework
├── resource/
│   └── Int20k.txt          # Test data (20,000 integers)
├── output/
│   └── results_problem4.txt # Performance results (generated)
└── README.md
```

## Implementation Details

### Doubly Linked List (`DynamicSet_LinkedList`)

**Structure:**

- Each element stored in a `Node` with `value`, `prev`, and `next` pointers
- `head` and `tail` pointers for efficient access
- Dynamic memory allocation

**Operations:**

- `add(x)` - O(n) to check existence, O(1) to add at tail
- `remove(x)` - O(n) to find and remove
- `is_element(x)` - O(n) linear search
- `set_empty()` - O(1) check if head is None
- `set_size()` - O(n) traverse and count

**Advantages:**

- No size limit
- Efficient insertion/deletion (once position found)
- No wasted memory

### Array (`DynamicSet_Array`)

**Structure:**

- Fixed-size array with sequential storage
- All `None` values stored at the end
- Compact representation

**Operations:**

- `add(x)` - O(n) to check existence + find empty slot
- `remove(x)` - O(n) to find + shift elements
- `is_element(x)` - O(n) with early termination possible
- `set_empty()` - O(n) worst case
- `set_size()` - O(n) count non-None values

**Advantages:**

- Cache-friendly (contiguous memory)
- Simple implementation
- Predictable memory usage

## Usage

### Running the Performance Test

```bash
cd src
python DynamicSet.py
```

The program will:

1. Load 20,000 integers from `resource/Int20k.txt`
2. Generate 100 random numbers to search for
3. Time each lookup operation for both implementations
4. Write results to `output/results_problem4.txt`
5. Display average lookup times
6. Generate a scatter plot visualisation

### Using as a Library

```python
from DynamicSet import DynamicSet_LinkedList, DynamicSet_Array

# Linked List implementation
ll_set = DynamicSet_LinkedList()
ll_set.add(10)
ll_set.add(20)
ll_set.add(30)
print(ll_set.is_element(20))  # True
ll_set.remove(20)
print(ll_set.set_size())      # 2

# Array implementation (size must be specified)
array_set = DynamicSet_Array(100)
array_set.add(10)
array_set.add(20)
array_set.add(30)
print(array_set.is_element(20))  # True
array_set.remove(20)
print(array_set.set_size())      # 2
```

## Performance Analysis

### Time Complexity

| Operation      | Linked List | Array | Notes                                 |
| -------------- | ----------- | ----- | ------------------------------------- |
| `add()`        | O(n)        | O(n)  | Both check for duplicates first       |
| `remove()`     | O(n)        | O(n)  | Array requires shifting after removal |
| `is_element()` | O(n)        | O(n)  | Linear search in both                 |
| `set_empty()`  | O(1)        | O(n)  | LL checks head pointer                |
| `set_size()`   | O(n)        | O(n)  | Both require traversal/counting       |

### Space Complexity

| Implementation | Space | Notes                                                   |
| -------------- | ----- | ------------------------------------------------------- |
| Linked List    | O(n)  | 3 pointers per element (value, prev, next)              |
| Array          | O(m)  | Where m is the fixed array size (may have unused space) |

### Empirical Results

Based on testing with 20,000 elements and 100 random lookups:

**Expected Findings:**

- **Array** typically performs slightly faster for `is_element()` due to:

  - Cache locality (contiguous memory)
  - Simpler iteration logic
  - Early termination when hitting `None` values

- **Linked List** has more overhead due to:
  - Pointer dereferencing
  - Non-contiguous memory (cache misses)
  - Additional memory per element

The actual performance difference is small for small-to-medium datasets but becomes more pronounced with larger sets.

## Visualisation

The scatter plot (`plotter.py`) shows:

- X-axis: Test number (1-100)
- Y-axis: Lookup time (milliseconds)
- Two series: Linked List vs Array times
- Visualises performance variance across random lookups

## Design Decisions

1. **Sequential Array Storage**: All non-None values stored contiguously for better cache performance
2. **Doubly Linked List**: Allows bidirectional traversal and efficient deletion
3. **No Duplicates**: Both implementations prevent duplicate values
4. **Fixed Array Size**: Demonstrates space-time tradeoff (could be made dynamic with resizing

)

## Requirements

```bash
pip install matplotlib  # For visualisation only
```

Core functionality requires Python 3.6+ with no external dependencies.

## Future Improvements

- [ ] Implement hash table-based set for O(1) operations
- [ ] Add set union, intersection, difference operations
- [ ] Implement self-balancing BST (AVL/Red-Black tree) comparison
- [ ] Add memory profiling alongside time profiling
- [ ] Support for dynamic array resizing
- [ ] Benchmark with varying dataset sizes
- [ ] Parallel performance testing

## Learning Objectives

This project demonstrates:

- Trade-offs between array and linked list implementations
- Empirical performance analysis
- Data structure selection based on use case
- Python class design and encapsulation
- Performance measurement techniques

## References

- Introduction to Algorithms (CLRS) - Chapter 10: Elementary Data Structures
- Data Structures and Algorithm Analysis - Mark Allen Weiss
